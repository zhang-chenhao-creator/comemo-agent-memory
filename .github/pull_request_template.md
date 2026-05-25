# Pull Request

## Summary

<!-- What changed? Keep this short. -->

## Change Type

- [ ] Documentation
- [ ] Template
- [ ] Adapter
- [ ] Example
- [ ] Compatibility note
- [ ] Release preparation
- [ ] Other

## Scope

- [ ] README
- [ ] docs
- [ ] templates/en
- [ ] templates/zh-CN
- [ ] adapters
- [ ] examples
- [ ] .github

## Validation

- [ ] Markdown renders correctly.
- [ ] All relative links point to existing files.
- [ ] English and Chinese templates remain structurally aligned when relevant.
- [ ] Chinese filenames remain readable as UTF-8 when relevant.
- [ ] Public behavior changes are reflected in `CHANGELOG.md`.

## comemo Constraints

- [ ] No `.sh`, `.ps1`, `.py`, binary installer, or package-manager installer was added to the core flow.
- [ ] `AGENTS.md` remains the fixed instruction filename.
- [ ] Adapters remain thin and do not duplicate the full memory system.
- [ ] Compatibility wording does not overpromise runtime behavior.
- [ ] Existing native memory files are treated as user assets and are not silently replaced.
