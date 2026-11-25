# librdkafka Repository Instructions

## Testing policy (required for every code change)

- Use librdkafka's **existing native C/C++ test framework** for all newly
  authored or modified tests, including unit, mock, and broker-backed
  regressions. Do not introduce GoogleTest, Catch2, or a second test runner or
  assertion framework. Existing coverage must not disappear when tests are
  moved or a test harness is removed.
- Read [tests/README.md](tests/README.md) before editing any production code,
  test, build option, or test-related CI configuration. Follow its section
  "Native testing policy and execution" for test selection and commands.
- Write or update a focused failing regression before the production fix when
  behavior changes. Use the existing native `TEST_ASSERT`/`TEST_FAIL` and
  `SUB_TEST` mechanisms for numbered tests, or the existing `rd_kafka_unittest`
  registry and `RD_UT_ASSERT` for internal unit tests. Do not bypass their
  result reporting or silently ignore failures.
- Broker-independent tests must be runnable without Kafka. Mark numbered tests
  `TEST_F_LOCAL`; explicitly distinguish a mock broker from a real Kafka
  integration test. A broker-backed claim requires a real broker-backed run.
- Preserve both Make and the original CMake/CTest entry points **that invoke
  the native test-runner**, Windows project registration where applicable, and
  the existing default CI behavior. Do not add standalone CTest/GTest suites.
  Perform verification in an isolated build directory; do not replace another
  run's build, test output, cluster, registry, or resources.
- Before handing off a change, report the exact test commands, test selection,
  pass/fail results, and coverage limitations. Do not describe a compile or
  preflight check as a passing regression test.

These requirements apply to future changes as well as this migration. For
contributor instructions, see [CONTRIBUTING.md](CONTRIBUTING.md).
