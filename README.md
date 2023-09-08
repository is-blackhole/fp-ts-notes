# fp-ts-notes

- TE.tapError: replace error with another one, right is not affected or can be changed
  ```
  async function testTapError() {
  const _testTapError = (te: TE.TaskEither<string, string>) =>
    pipe(
      te,
      TE.tapError((e) => {
        switch (e) {
          case "error to replace":
            return TE.left("replaced error");
          case "go right":
            return TE.right(e);
          default:
            return TE.left(e);
        }
      })
    );

  assert.deepStrictEqual(await _testTapError(TE.right("ok"))(), E.right("ok"));
  assert.deepStrictEqual(await _testTapError(TE.left("error to replace"))(), E.left("replaced error"));
  assert.deepStrictEqual(await _testTapError(TE.left("passed error"))(), E.left("passed error"));
  assert.deepStrictEqual(await _testTapError(TE.left("go right"))(), E.left("go right"));
}

testTapError();
  ```
- 
