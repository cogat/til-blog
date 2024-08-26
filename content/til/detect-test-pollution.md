---
title: "Finding one polluting test among thousands of options"
date: 2024-08-26T14:39:15+10:00
---

Sometimes, a test can leave the environment changed in a way that causes other tests to fail. This is known as "test pollution". Finding a polluting test can be particularly annoying, because every test passes on its own; it's only when the tests are run in _some order_, with the unknown polluting test before a known polluted test, that a failure occurs.

There's a tool that will track down a polluting test: [`detect-test-pollution`](https://github.com/asottile/detect-test-pollution/). Tell this tool which test is failing, and it runs the test after smaller and smaller sets of other tests (known as bisecting, or binary search), until it is left with only one result, namely the polluting test.

I ended up using a two-part process to create the test IDs first, like this:

```shell
export DJANGO_CONFIGURATION=MyConfiguration
py.test -q --collect-only path/to/tests > test_ids.txt
detect-test-pollution \
    --failing-test path/to/test.py::TestClass::test_name \
    --testids-file test_ids.txt
```

 After several minutes of narrowing down the list of suspects, it finally nailed the exact one!

Creating the IDs first made it faster to debug my way through some of the quirks, described below.

## Getting it working with `pytest` customisations

The tool exhibits a couple of quirks when it is run against our codebase at work, which has a few pytest customisations. To get it running, I needed to:

1. Temporarily remove `--verbose` from our `pytest.ini` defaults, to fix the test_ids format. (The `test_ids.txt` file created below should contain a plain list of IDs, not a angle-bracketed hierarchical format.)
2. Ensure that the tests run without errors first, mainly to ensure that the database is up-to-date (failing tests are OK at this point, but we don't want errors).
3. Run the `detect-test-pollution` command with `DJANGO_CONFIGURATION` set, so the subprocess pytest commands know which configuration to use.
