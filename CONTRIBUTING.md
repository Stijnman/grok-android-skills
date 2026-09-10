# Contributing Guide

Thank you for your interest in contributing to **hermes-prompts**!
This document outlines how to contribute new prompts, improve existing ones, and help maintain this library.

---

## 📋 Table of Contents

- [Code of Conduct](#-code-of-conduct)
- [How to Contribute](#-how-to-contribute)
- [Adding a New Prompt](#-adding-a-new-prompt)
- [Improving Existing Prompts](#-improving-existing-prompts)
- [Testing Requirements](#-testing-requirements)
- [Pull Request Process](#-pull-request-process)
- [Review Process](#-review-process)

---

## 🤝 Code of Conduct

By participating in this project, you agree to abide by the [Contributor Covenant Code of Conduct](CODE_OF_CONDUCT.md).
We are committed to providing a welcoming and inspiring community for all.

---

## 🚀 How to Contribute

### Reporting Issues

If you find an issue with a prompt, please [open an issue](https://github.com/Stijnman/hermes-prompts/issues/new) with:
- Clear description of the problem
- Which prompt is affected
- What happened vs what you expected
- Any error messages

### Suggesting Enhancements

For feature requests or improvements:
1. Check existing issues for duplicates
2. Open a new issue with:
   - Detailed description of the enhancement
   - Use case or problem it solves
   - Proposed solution (if you have one)

### Contributing Code/Prompts

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/your-prompt`)
3. Make your changes
4. Add documentation
5. Commit your changes
6. Push to your fork
7. Open a Pull Request

---

## ✨ Adding a New Prompt

### Before You Start

1. **Check for duplicates**: Search existing prompts to ensure the capability isn't already covered
2. **Verify usefulness**: Ensure the prompt provides value and isn't redundant
3. **Test manually**: Verify the prompt works with available AI models

### Prompt Structure

Every prompt should follow this structure:

```markdown
## Prompt Name

**Purpose**: Clear description of what this prompt does

**Use When**: When to use this prompt

**Don't Use When**: When NOT to use this prompt

**Prompt**:
```
[The actual prompt text goes here]
```

**Example Usage**:
```
User: [example input]
AI: [example output]
```

**Notes**:
- Any additional notes or warnings
```

### Prompt Requirements

Every new prompt **MUST** include:
1. Clear name and purpose
2. Usage guidelines (when to use/when not to use)
3. The prompt text itself
4. Example usage
5. Any relevant notes or warnings

### Content Guidelines

**DO:**
- Use clear, concise language
- Include specific instructions
- Add context when helpful
- Include examples
- Add safety disclaimers when needed

**DON'T:**
- Include sensitive or personal data
- Request inappropriate information
- Encourage illegal or unethical behavior
- Make promises the AI can't keep
- Use overly complex or confusing language

---

## 🔧 Improving Existing Prompts

### Before Submitting Changes

1. **Verify the issue**: Ensure the change addresses a real problem
2. **Check existing PRs**: Avoid duplicate work
3. **Test locally**: Verify your changes work as expected

### Types of Improvements

- Fix typos or unclear language
- Add missing examples
- Clarify ambiguous instructions
- Add warnings or notes
- Improve prompt structure
- Enhance prompt effectiveness
- Add cross-references

---

## 🧪 Testing Requirements

All contributions **MUST** be tested. At minimum:

### Manual Testing
- [ ] Prompt works with valid inputs
- [ ] Prompt handles edge cases
- [ ] Prompt produces quality output
- [ ] Prompt is safe and appropriate

### Documentation
- [ ] Prompt is properly documented
- [ ] Examples are clear
- [ ] Usage guidelines are provided

---

## 📤 Pull Request Process

### 1. Fork and Branch

```bash
git clone https://github.com/YOUR_USERNAME/hermes-prompts.git
cd hermes-prompts
git checkout -b feature/your-prompt-name
```

### 2. Make Changes

- Add your new prompt or improve existing one
- Add documentation
- Update any relevant files

### 3. Commit Messages

Follow [Conventional Commits](https://www.conventionalcommits.org/) format:

```
feat: add new reasoning prompt for complex problems
fix: correct typo in coding prompt
docs: update README with new prompts
test: add tests for new prompts
```

**Guidelines:**
- Use present tense
- Limit first line to 50 characters
- Separate subject from body with blank line
- Wrap body at 72 characters

### 4. Push Changes

```bash
git push origin feature/your-prompt-name
```

### 5. Open Pull Request

1. Go to https://github.com/Stijnman/hermes-prompts
2. Click "New Pull Request"
3. Select your fork and feature branch
4. Fill in PR template
5. Click "Create Pull Request"

---

## 🎯 Pull Request Template

```markdown
## Description

[Clear description of the changes]

## Type of Change

- [ ] New prompt
- [ ] Prompt improvement
- [ ] Documentation update
- [ ] Bug fix
- [ ] Other: _______________

## Testing

- [ ] Manual testing completed
- [ ] Prompt tested with multiple inputs
- [ ] Output quality verified
- [ ] Safety considerations reviewed

## Checklist

- [ ] Code follows repository standards
- [ ] I have read CONTRIBUTING.md
- [ ] Documentation added
- [ ] All tests pass
- [ ] No sensitive data
- [ ] All links work
```

---

## 🔍 Review Process

1. **Maintainer Review**: Repository maintainer reviews the PR
2. **Feedback**: You may receive requests for changes
3. **Approval**: PR is approved and merged

### Review Criteria

- [ ] Follows repository standards
- [ ] Clear and readable
- [ ] Well-documented
- [ ] Ethically sound
- [ ] Safe and appropriate

---

## 🛠️ Maintenance

### Versioning
- **MINOR**: New prompts or significant improvements
- **PATCH**: Bug fixes and documentation updates

### Organization
- Keep prompts well-organized by category
- Maintain consistent formatting
- Update cross-references
- Archive deprecated prompts

---

*Thank you for contributing! Your help makes this library better for everyone.*

*Last updated: September 11, 2026*
