# axe-testcafe
The TestCafe module that allows you to use the [aXe](https://github.com/dequelabs/axe-core) accessibility engine in TestCafe tests.

This project was forked from [axe-testcafe](https://github.com/helen-dikareva/axe-testcafe) which has been dormant for quite some time.

## Installation

```bash
npm install axe-core axe-testcafe --save-dev
```

## How to use

You can write a TestCafe test with automated accessibility checks like this.

```js
import { axeCheck, createReport } from 'axe-testcafe';

fixture `TestCafe tests with Axe`
    .page `http://example.com`;

test('Automated accessibility testing', async t => {
    const { error, violations } = await axeCheck(t);
    await t.expect(violations.length === 0).ok(createReport(violations));
});
```

If any accessibility issues are found, you will see a detailed report generated by the `createReport` function.

![Accessibility errors](https://github.com/helen-dikareva/axe-testcafe/blob/master/errors.png)

## aXe options

The `axe-testcafe` module allows you to define the `context` and `options` [axe.run parameters](https://github.com/dequelabs/axe-core/blob/develop/doc/API.md#api-name-axerun) in a TestCafe test.

```js
test('Automated accessibility testing', async () => {
    const axeContext = { exclude: [['select']] };
    const axeOptions = { rules: { 'html-has-lang': { enabled: false } } };
    const { error, violations } = await axeCheck(t, axeContext, axeOptions);
    await t.expect(violations.length === 0).ok(createReport(violations));
});
