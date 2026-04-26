# Test Generator

Auto-generate tests for executed code using MCP servers.

## Trigger

- "generate tests"
- "write tests"
- "add test coverage"
- Post-execution phase

## What It Does

1. **Analyze** the generated code
2. **Identify** testable functions
3. **Generate** unit tests
4. **Generate** integration tests
5. **Run** tests to verify

## Test Types

### Unit Tests
```typescript
describe('UserService', () => {
  it('should create user', async () => {
    const user = await createUser({ name: 'Test' });
    expect(user.id).toBeDefined();
  });
});
```

### Integration Tests
```typescript
describe('API', () => {
  it('POST /users returns 201', async () => {
    const res = await request.post('/users').send({ name: 'Test' });
    expect(res.status).toBe(201);
  });
});
```

## Test Framework Detection

Auto-detect from project:
- Vitest
- Jest
- Mocha
- Playwright

## Coverage Target

- minimum 80% coverage
- All exported functions tested
- Edge cases covered
- Error paths tested

## Execution

```bash
# Generate tests for a file
/gsd-test-generate src/user.ts

# Run generated tests
/gsd-test-run

# Check coverage
/gsd-test-coverage
```

## Boundaries

- Don't overwrite existing tests
- Generate adjacent .test.ts files
- Validate tests pass after generation