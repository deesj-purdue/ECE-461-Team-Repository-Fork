# Unit Tests for ECE-461 Team Repository

This directory contains comprehensive unit tests for the ECE-461 Team Repository AI/ML Model Evaluation System.

## 📋 Test Structure

```
tests/
├── __init__.py                      # Test package initialization
├── test_base_metric.py             # Tests for BaseMetric abstract class
├── test_url_handlers.py            # Tests for URL handler classes
├── test_repo_context.py            # Tests for RepoContext dataclass
├── test_metric_eval.py             # Tests for MetricEval orchestrator
├── test_net_scorer.py              # Tests for NetScorer (weighted scoring)
├── test_error_handling.py          # Comprehensive error handling tests
├── test_community_rating_metric.py # Tests for CommunityRatingMetric
├── test_extended_metrics.py        # Tests for all extended metrics
├── test_integration.py             # Integration tests for complete system
├── test_cli_layer.py               # CLI layer tests
├── test_routing_layer.py           # URL routing tests
├── test_run_install.py             # Installation script tests
└── test_run_test.py                # Test runner tests
```

## 🚀 Running Tests

### Prerequisites
First, install the testing dependencies:
```bash
pip install pytest pytest-cov pytest-mock
```

### Run All Tests
```bash
# From project root directory
python -m pytest tests/ -v

# Run with coverage report
python -m pytest tests/ --cov=src --cov-report=html --cov-report=term-missing

# Run only working tests (exclude known failing ones)
python -m pytest tests/test_url_handlers.py tests/test_repo_context.py tests/test_metric_eval.py tests/test_net_scorer.py tests/test_error_handling.py tests/test_integration.py tests/test_extended_metrics.py tests/test_base_metric.py tests/test_community_rating_metric.py -v
```

### Run Specific Test Files
```bash
# Core functionality tests
python -m pytest tests/test_url_handlers.py -v       # URL handler classes
python -m pytest tests/test_repo_context.py -v       # Repository context
python -m pytest tests/test_metric_eval.py -v        # Metric evaluation
python -m pytest tests/test_net_scorer.py -v         # Weighted scoring
python -m pytest tests/test_error_handling.py -v     # Error handling

# Metric tests
python -m pytest tests/test_base_metric.py -v        # BaseMetric abstract class
python -m pytest tests/test_community_rating_metric.py -v  # Community metrics
python -m pytest tests/test_extended_metrics.py -v   # All extended metrics

# Integration tests
python -m pytest tests/test_integration.py -v        # Full system integration
```

### Run Tests with Coverage
```bash
python -m pytest tests/ --cov=src --cov-report=html --cov-report=term-missing
```

## 📊 Test Coverage

The test suite covers:

### BaseMetric Tests (`test_base_metric.py`)
- ✅ Abstract class cannot be instantiated
- ✅ Concrete implementations work correctly
- ✅ Initialization with different weights
- ✅ String representation
- ✅ Error handling for evaluation failures
- ✅ Variable input handling

### MetricEval Tests (`test_metric_eval.py`)
- ✅ Initialization with metrics and weights
- ✅ Parallel evaluation of multiple metrics
- ✅ Score aggregation with proper weighting
- ✅ Error handling for failing metrics
- ✅ Edge cases (empty inputs, unicode names, etc.)
- ✅ Concurrent execution testing

### CommunityRatingMetric Tests (`test_community_rating_metric.py`)
- ✅ Logarithmic scaling of likes and downloads
- ✅ Handling missing data gracefully
- ✅ Score clamping to [0.0, 1.0] range
- ✅ Realistic scenario testing
- ✅ Mathematical correctness of scoring

### Integration Tests (`test_integration.py`)
- ✅ Complete evaluation pipeline
- ✅ Multiple model evaluation
- ✅ Error handling in full system
- ✅ Weight impact verification
- ✅ Performance with many metrics

## 🎯 Test Categories

### Unit Tests
- Test individual components in isolation
- Mock external dependencies
- Fast execution (< 1 second per test)

### Integration Tests  
- Test components working together
- Use real implementations
- May be slower but test real scenarios

### Performance Tests
- Marked with `@pytest.mark.slow`
- Test system scalability
- Can be skipped with: `pytest -m "not slow"`

## 📈 Expected Test Results

When all tests pass, you should see output like:
```
tests/test_base_metric.py::TestBaseMetric::test_base_metric_cannot_be_instantiated PASSED
tests/test_base_metric.py::TestBaseMetric::test_concrete_metric_initialization PASSED
tests/test_metric_eval.py::TestMetricEval::test_metric_eval_initialization PASSED
tests/test_community_rating_metric.py::TestCommunityRatingMetric::test_initialization PASSED
tests/test_integration.py::TestIntegrationMetricsSystem::test_full_evaluation_pipeline PASSED

========================= XX passed in X.XXs =========================
```

## 🐛 Debugging Failed Tests

### Common Issues
1. **Import Errors**: Ensure you're running from project root and have proper Python path
2. **Missing Dependencies**: Run `pip install -r requirements.txt`
3. **Path Issues**: Check that file paths in tests match your project structure

### Verbose Output
For more detailed output when tests fail:
```bash
python -m pytest tests/ -vvs --tb=long
```

### Running Single Test
To debug a specific test:
```bash
python -m pytest tests/test_base_metric.py::TestBaseMetric::test_initialization -vvs
```

## 📝 Adding New Tests

When adding new metrics or functionality:

1. **Create test file**: `test_your_new_metric.py`
2. **Follow naming convention**: `TestYourNewMetric` class
3. **Test all public methods**: Especially `evaluate()` and `get_description()`
4. **Test edge cases**: Empty inputs, invalid data, etc.
5. **Add integration test**: Show it works with MetricEval

### Test Template
```python
import pytest
from src.metrics.your_metric import YourMetric

class TestYourMetric:
    def test_initialization(self):
        metric = YourMetric()
        assert metric.name == "expected_name"
        assert metric.weight == expected_weight
    
    def test_evaluate_basic(self):
        metric = YourMetric()
        result = metric.evaluate({"test": "data"})
        assert 0.0 <= result <= 1.0
```

## 🔧 Configuration

Test configuration is in `pytest.ini`:
- Test discovery patterns
- Output formatting
- Marker definitions
- Coverage settings (when enabled)

## 📊 Metrics for Success

A good test suite should have:
- ✅ **High Coverage**: >90% line coverage
- ✅ **Fast Execution**: Most tests < 100ms
- ✅ **Clear Failures**: Easy to understand what went wrong
- ✅ **Comprehensive**: Cover happy path, edge cases, and error conditions
