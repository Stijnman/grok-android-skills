# Testing Guide

This document outlines the testing requirements and best practices for the **hermes-prompts** project.

---

## 📋 Table of Contents

- [Testing Philosophy](#-testing-philosophy)
- [Testing Levels](#-testing-levels)
- [Manual Testing](#-manual-testing)
- [Automated Testing](#-automated-testing)
- [Test Checklists](#-test-checklists)

---

## 🎯 Testing Philosophy

### Core Principles

1. **Quality First**: Ensure all prompts produce high-quality, useful output
2. **Safety**: Verify prompts don't generate harmful or inappropriate content
3. **Effectiveness**: Test that prompts achieve their intended purpose
4. **Clarity**: Ensure prompts are clear and unambiguous
5. **Documentation**: All tests should be documented

### What Must Be Tested

Every prompt **MUST** be tested for:
- ✅ Output quality and usefulness
- ✅ Content safety and appropriateness
- ✅ Clarity and specificity
- ✅ Ethical considerations
- ✅ Bias and fairness
- ✅ Consistency across runs

---

## 🏗️ Testing Levels

### Level 1: Unit Testing (Prompt Validation)

Test individual prompts for correctness and quality.

**Example**: Testing a reasoning prompt
```python
# tests/test_prompts.py
import pytest
from prompts import REASONING_PROMPT, CODING_PROMPT


def test_reasoning_prompt_structure():
    """Test that reasoning prompt has required structure"""
    assert "You are" in REASONING_PROMPT
    assert "Please reason" in REASONING_PROMPT
    assert len(REASONING_PROMPT) > 100


def test_coding_prompt_has_instructions():
    """Test that coding prompt includes instructions"""
    assert "write" in CODING_PROMPT.lower() or "create" in CODING_PROMPT.lower()
    assert "code" in CODING_PROMPT.lower()
```

### Level 2: Integration Testing

Test prompts in context with actual AI responses.

**Example**: Testing prompt output quality
```python
# tests/test_output_quality.py
import pytest
from ai_client import generate_response


def test_reasoning_prompt_output():
    """Test that reasoning prompt produces thoughtful output"""
    response = generate_response(REASONING_PROMPT + "\n\nExplain quantum computing")
    
    # Check for quality indicators
    assert len(response) > 100
    assert "quantum" in response.lower()
    assert any(word in response.lower() for word in ["qubit", "superposition", "entanglement"])
```

### Level 3: End-to-End Testing

Test the complete user experience with prompts.

**Manual Test Script**:
```
1. Select a prompt from the library
2. Apply the prompt to a test scenario
3. Review the generated output
4. Evaluate quality, safety, and effectiveness
5. Document any issues
```

---

## 👤 Manual Testing

### Required Manual Tests

For **every prompt**, manually test:

#### Quality Tests
- [ ] Prompt produces relevant output
- [ ] Prompt produces coherent output
- [ ] Prompt produces useful output
- [ ] Prompt is clear and understandable

#### Safety Tests
- [ ] No harmful content generated
- [ ] No inappropriate content generated
- [ ] No biased content generated
- [ ] No sensitive data exposed

#### Consistency Tests
- [ ] Similar inputs produce similar outputs
- [ ] Prompt works across different scenarios
- [ ] Prompt handles edge cases

### Manual Testing Checklist Template

```markdown
# Testing Checklist: [Prompt Name]

## Setup
- [ ] AI model available
- [ ] Test environment configured
- [ ] Test scenarios prepared

## Quality Tests
- [ ] Test 1: Basic usage
- [ ] Test 2: Complex scenario
- [ ] Test 3: Edge case
- [ ] Test 4: Error handling

## Safety Tests
- [ ] No harmful content: _______________
- [ ] No inappropriate content: _____________
- [ ] No biased content: _______________
- [ ] No sensitive data: ______________

## Results
- [ ] All tests passed
- [ ] Issues found: _______________
- [ ] Notes: _____________________
```

---

## 🤖 Automated Testing

### Test File Structure

```
hermes-prompts/
├── tests/
│   ├── __init__.py
│   ├── conftest.py          # Fixtures and setup
│   ├── test_prompts.py      # Prompt structure tests
│   ├── test_quality.py      # Output quality tests
│   └── test_safety.py       # Safety and ethics tests
```

---

## ✅ Test Checklists

### New Prompt Checklist

Before adding a new prompt to the library:

- [ ] Prompt has clear purpose and description
- [ ] Prompt is well-structured
- [ ] Prompt has been manually tested
- [ ] Prompt produces quality output
- [ ] Prompt has safety considerations
- [ ] Prompt is documented
- [ ] Prompt follows library standards

### Existing Prompt Update Checklist

Before updating an existing prompt:

- [ ] Changes tested with existing functionality
- [ ] No breaking changes (or documented if breaking)
- [ ] Version bumped appropriately
- [ ] Changelog updated
- [ ] Documentation updated

### Pre-PR Checklist

Before opening a pull request:

- [ ] All manual tests pass
- [ ] Automated tests pass (if applicable)
- [ ] Code follows repository standards
- [ ] Documentation is complete
- [ ] No sensitive data committed
- [ ] All links work

---

## 🎯 Summary

| Aspect | Requirement |
|--------|-------------|
| Manual Testing | ✅ Required for all prompts |
| Automated Testing | ⚠️ Recommended for all prompts |
| Quality Testing | ✅ Required |
| Safety Testing | ✅ Required |
| Documentation | ✅ Required |

**Remember**: The quality of your prompts directly impacts the effectiveness and safety of AI-generated content.

---

*Last updated: September 11, 2026*
