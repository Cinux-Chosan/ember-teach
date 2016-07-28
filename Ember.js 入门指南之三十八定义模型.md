ģ��Ҳ��һ���࣬�����������û�չʾ�����Ժ�������Ϊ��ģ�͵Ķ���ǳ��򵥣�ֻ��Ҫ�̳�[DS.Model](http://emberjs.com/api/data/classes/DS.Model.html)�༴�ɣ�������Ҳ����ֱ��ʹ��[Ember CLI](http://ember-cli.com/user-guide)�����������ʹ������ģ�� `ember g model person`������һ��ģ����`person`��
```js
//  app/models/person.js

import DS from 'ember-data';

export default DS.Model.extend({
  
});
```
����Ǹ��յ�ģ�ͣ�û�ж����κ����ԡ�����ģ������Ϳ���ʹ��`find`�������������ˡ�

## 1����������

���涨���ģ����`person`��û���κ����ԣ�����Ϊ�������Ӽ������ԡ�
```js
//  app/models/person.js

import DS from 'ember-data';

export default DS.Model.extend({
	firstName: DS.attr(),
	lastName: DS.attr(),
	birthday: DS.attr()  
});
```
�������붨����3�����ԣ����ǻ�δ������ָ�����ͣ�Ĭ�϶���`string`���͡���Щ�������������ӵķ������ϵ�����`key`��һ�µġ������㻹������ģ���ж���[��������](http://blog.ddlisting.com/2016/03/17/ember-js-ru-men-zhi-nan-ji-suan-shu-xing-compute-properties/)��
```js
//  app/models/person.js

import DS from 'ember-data';

export default DS.Model.extend({
	firstName: DS.attr(),
	lastName: DS.attr(),
	birthday: DS.attr(),

	fullName: Ember.computed('firstName', 'lastName', function() {
		return `${this.get('firstName')} ${this.get('lastName')}`;
	})
});
```
��δ�����ģ�����ж�����һ����������`fullName`��

## 2��ָ������������Ĭ��ֵ

ǰ�涨���ģ������û��ָ���������͵ģ�Ĭ������¶���`string`���ͣ���Ȼ���ǲ����ģ��򵥵�ģ���������Ͱ�����`string`��`number`��`boolean`��`date`���⼸���������벻���ҽ��Ͷ�Ӧ��֪���ˡ�

��������ָ���������ͣ��㻹����ָ�����Ե�Ĭ��ֵ����[attr()](http://emberjs.com/api/data/classes/DS.html#method_attr)�����ĵڶ�������ָ������������Ĵ��룺
```js
//  app/models/person.js

import DS from 'ember-data';

export default DS.Model.extend({
	username: DS.attr('string'),
	email: DS.attr('string'),
	verified: DS.attr('boolean', { defaultValue: false }),  //ָ��Ĭ��ֵ��false
	//  ʹ�ú�������ֵ��ΪĬ��ֵ
	createAt: DS.attr('string', { defaultValue(){ return new Date(); } })
});
```
�������ע�������ģ�����Ĭ��ֵ�ķ�ʽ����ֱ��ָ��������ʹ�ú�������ֵָ����

## 3������ģ�͵Ĺ�����ϵ
	
[Ember](http://emberjs.com)��ģ��Ҳ�������������ݿ�Ĺ�����ϵ�ġ�ֻ������ڸ��Ƶ����ݿ�[Ember](http://emberjs.com)��ģ�;��Եü򵥺ܶ࣬���а���һ��һ��һ�Զ࣬��Զ������ϵ�����ֹ�ϵ�����̨�����ݿ�����ͳһ�ġ�

#### 1��һ��һ

����һ��һ����ʹ��[DS.belongsTo](http://emberjs.com/api/data/classes/DS.html#method_belongsTo)���á��������������ģ�͡�
```js
//  app/models/user.js
import DS from 'ember-data';

export default DS.Model.extend({
  profile: DS.belongsTo(��profile��);
});
```
```js
//  app/models/profile.js
import DS from ��ember-data��;
export default DS.Model.extend({
  user: DS.belongsTo(��user��);
});
```

#### 2��һ�Զ�
	
����һ�Զ����ʹ��[DS.belongsTo](http://emberjs.com/api/data/classes/DS.html#method_belongsTo)�����һ��ʹ�ã���[DS.hasMany](http://emberjs.com/api/data/classes/DS.html#method_hasMany)���ٵ�һ��ʹ�ã����á��������������ģ�͡�
```js
//  app/models/post.js
import DS from ��ember-data��;
export default DS.Model.extend({
  comments: DS.hasMany(��comment��);
});
```
���ģ����һ��һ���������ģ���Ƕ��һ����
```js
//  app/models/comment.js
import DS from ��ember-data��;
export default DS.Model.extend({
  post: DS.belongsTo(��post��);
});
```
�������õķ�ʽ��Java ��hibernate�ǳ����ơ�

#### 3����Զ�

����һ�Զ����ʹ��[DS.hasMany](http://emberjs.com/api/data/classes/DS.html#method_hasMany)���á��������������ģ�͡�
```js
//  app/models/post.js
import DS from ��ember-data��;
export default DS.Model.extend({
  tags: DS.hasMany(��tag��);
});
```
```js
//  app/model/tag.js
import DS from ��ember-data��;
export default DS.Model.extend({
  post: DS.hasMany(��post��);
});
```
��Զ�Ĺ�ϵ���ö���ʹ��[DS.hasMany](http://emberjs.com/api/data/classes/DS.html#method_hasMany)�����ǲ�����Ҫ���м������������ݵĶ�Զ��е㲻ͬ����������ݵĶ�Զ�ͨ����ͨ���м�������

## 4����ʽ��ת

[Ember Data](https://github.com/emberjs/data)�ᾡ��ȥ��������ģ��֮��Ĺ�����ϵ������ǰ���һ�Զ��ϵ�У���`comment`�����仯��ʱ����Զ����µ�`post`����Ϊÿһ��`comment`ֻ��Ӧһ��`post`��������`comment`ȷ����ĳ��һ��`post`��

Ȼ������ʱ��ͬһ��ģ���л��ж����˹���ģ�͡���ʱ������ڷ������[DS.hasMany](http://emberjs.com/api/data/classes/DS.html#method_hasMany)��`inverse`ѡ��ָ���������ģ�ͣ�
```js
//  app/model/comment.js
import DS from 'ember-data';
export default DS.Model.extend({
  onePost: DS.belongsTo(��post��),
  twoPost: DS.belongsTo(��post��),
  redPost: DS.belongsTo(��post��),
  bluePost: DS.belongsTo(��post��)
});
```
��һ��ģ����ͬʱ��3��`post`�����ˡ�
```js
//  app/models/post.js
import DS from ��ember-data��;
export default DS.Model.extend({
  comments: hasMany(��comment��, { inverse: ��redPost�� });
});
```
��`comment`�����仯ʱ�Զ����µ�`redPost`���ģ�͡�

## 5���Է���ϵ

#### 1��һ�Զ�

�����붨��һ���Է���ϵ��ģ��ʱ��ģ�ͱ����һ��һ��ϵ���������Ҫ��ʽʹ��`inverse`ָ��������ģ�͡����û�������ϵ���`inverse`ֵ����Ϊ`null`��
```js
//  app/models/folder.js
import DS from ��ember-data��;
export default DS.Model.extend({
  children: DS.hasMany(��folder��, { reverse: ��parent�� });
  parent: DS.hasMany(��folder��, { reverse: ��children�� });
});
```
һ���ļ���ͨ���и��ļ��л������ļ��С���ʱ���ļ��к����ļ����뱾����ͬһ�����͵�ģ�͡���ʱ����Ҫ��ʽʹ��`inverse`����ָ����������δ�����ʾ����children���������д�����˼�����ģ����һ������`children`�������������Ҳ��һ��`folder`��ģ�ͱ�����Ϊ���ļ��С�ͬ��parent���������д������˼�����ģ���и�����`parent`�������������Ҳ��һ��`folder`��ģ�ͱ�����������Ե����ļ��С�������ͼ�ṹ��

![�ṹͼ](/content/images/2016/04/140.png)

����е������ݽṹ�е���������԰�`children`��`parent`�������һ��ָ�롣

������й�����ϵû�������ϵֱ�Ӱ�`inverse`����Ϊ`null`��
```js
//  app/models/folder.js
import DS from ��ember-data��;
export default DS.Model.extend({
  parent: DS.belongsTo(��folder��, { inverse: null });
});
```

#### 2��һ��һ

```js
//  app/models/user.js
import DS from ��ember-data��;
export default DS.Model.extend({
  bestFriend: DS.belongsTo(��folder��, { inverse: ��bestFriend�� });
});v
```
�����ϵ�����ݿ����������˫��һ��һ�����ơ�

## 6��Ƕ������

��Щģ�Ϳ��ܻ�������Ƕ�׵����ݶ������Ҳ��ʹ�������Ĺ�����ϵ������ô���Ǹ�ج�Σ����������������ǰ����ݶ���ɼ򵥶�����Ȼ���ӵ��������ݵ��ǽ����˲�Ρ�����һ���ǰ�Ƕ�׵����ݶ����ģ�͵����ԣ�Ҳ���������൫�ǽ�����Ƕ�ײ�Σ���
<br>
���������������[Github](https://github.com/ubuntuvim/my_emberjs_code)�����ľ�������޸ģ������ϵĴ�����github��������г��룬����Ӱ�첻�󣡣����������ò��Ķ����е��ã�����github��Ŀ�ϸ��ҵ��`star`�ɡ����Ŀ϶�������˵�����Ķ�������









