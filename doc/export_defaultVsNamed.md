====== default =========

1 エラー できない
export default const InvalidError =  {
    InvalidTopicIdError,
    InvalidAudioError
};

2 constと分けるとできる
const InvalidError =  {
    InvalidTopicIdError,
    InvalidAudioError
};
export default InvalidError

import InvalidError from '../errors/InvalidError';
new InvalidError.InvalidTopicIdError()
new InvalidError.AbstractClassError()

3 匿名エクスポート 非推奨 自動インポート使えない
export default {
    InvalidTopicIdError,
    InvalidAudioError
};

import InvalidError from '../errors/InvalidError';
new InvalidError.InvalidTopicIdError()
new InvalidError.InvalidAudioError()

4 defaultをexportしてない、commonjs形式のモジュール
→[tsconfigにてesModuleInteropフラグを有効にすると、コンパイル時にヘルパーメソッドが生成されるようになり、モジュールシステムの相互運用性が高まる。](https://numb86-tech.hatenablog.com/entry/2020/07/11/160159)
これにより、defaultをエクスポートしていない CommonJS 形式のモジュールを、ES Modules でデフォルトインポートする、といったことが可能になる。

modules.exports = {
    InvalidTopicIdError,
    InvalidAudioError
};
or
export = {
    InvalidTopicIdError,
    InvalidAudioError
};

import InvalidError = require('../errors/InvalidError')
or
import InvalidError from ('../errors/InvalidError')
new InvalidError.InvalidTopicIdError()
new InvalidError.InvalidAudioError()

====== named =========

5 定義時に都度export
export class InvalidInstanceError extends ComomonError {}
export class AbstractClassError extends ComomonError {}

import { InvalidInstanceError, AbstractClassError } from '../errors/InvalidError';
new InvalidInstanceError()
new AbstractClassError()

6 まとめてもできる
export {
    InvalidTopicIdError,
    InvalidAudioError
};

import { InvalidTopicIdError, InvalidAudioError } from '../errors/InvalidError';
new InvalidTopicIdError()


import { InvalidTopicIdError, InvalidAudioError } = require('../errors/InvalidError');
new InvalidTopicIdError()

7 defaultっぽいnamed
export const InvalidError =  {
    InvalidTopicIdError,
    InvalidAudioError
};

import { InvalidError } from '../errors/InvalidError';
new InvalidError.InvalidTopicIdError()
new InvalidError.AbstractClassError()