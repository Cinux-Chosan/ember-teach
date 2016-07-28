��ǰ��[Ember.js ����ָ��֮��ʮ�˶���ģ��](http://blog.ddlisting.com/2016/04/08/ding-yi-mo-xing/)�н��ܹ�ģ��֮ǰ�Ĺ�ϵ����Ҫ����һ��һ��һ�Զࡢ��Զ��ϵ�����ǻ�û���������й�����ϵģ�͵ĸ��¡�ɾ���Ȳ�����

Ϊ�˲����½�����ģ���ࡣ
```
ember g model post
ember g model comment
```
## 1��������ϵ��¼

```js
//  app/models/post.js

import DS from 'ember-data';

export default DS.Model.extend({
  comments: DS.hasMany('comment')
});

//  app/model/comment.js

import DS from 'ember-data';

export default DS.Model.extend({
  	post: DS.belongsTo('post')
});
```
���ù�������ϵ��ά�����ڶ��һ��`comment`�ϡ�
```js
let post = this.store.peekRecord('post', 1);
let comment = this.store.createRecord('comment', {
  post: post
});
comment.save();
```
����֮��`post`���Զ�������`comment`�ϣ�����`post`��`id`����ֵ��`post`�����ϣ���

��Ȼ����������ڴ�`post`�����ù�����ϵ����������Ĵ��룺
```js
let post = this.store.peekRecord('post', 1);
let comment = this.store.createRecord('comment', {
	//  ��������ֵ
});
//  �ֶ��ɶ������õ�post�����С���post�Ƕ��һ����comments����Ӧ���Ǳ����ϵ�����飩
post.get('comments').pushObject(comment);
comment.save();
```
�����ѧ��Java���hibernate���������������׾��������δ��롣���������`post`��һ��һ���������Ҫά����ϵ�ǲ���Ҫ�����������`comment`��`id`���浽`comments`���ԣ����飩�ϣ���Ϊһ��`post`���Թ������`comment`������`comments`����Ӧ����һ�����顣

## 2�������Ѿ����ڵļ�¼

���¹�����ϵ�봴��������ϵ������һ���ġ�Ҳ�����Ȼ�ȡ��Ҫ������ģ�����������ǵĹ�����ϵ��
```js
let post = this.store.peekRecord('post', 100);
let comment = this.store.peekRecord('comment', 1);
comment.set('psot', post);  //  ��������comment��post�Ĺ�ϵ
comment.save();  //  ��������Ĺ�ϵ
```
����ԭ��`comment`������`post`��`id`Ϊ`1`�����ݣ��������¸���Ϊ`comment`����`id`Ϊ`100`��`post`���ݡ�

����Ǵ�`post`�����£���ô�����������Ĵ���������
```js
let post = this.store.peekRecord('post', 100);
let comment this.store.peekRecord('comment', 1);
post.get('comments').pushObject(comment);  // ���ù���
post.save();  //  �������
```

## 3��ɾ��������ϵ

��Ȼ��������ϵ��ȻҲ����ɾ��������ϵ��
���Ҫ�Ƴ�����ģ�͵Ĺ�����ϵ��ֻ��Ҫ�ѹ���������ֵ����Ϊ`null`�Ϳ����ˡ�
```js
let comment = this.store.peekRecord('comment', 1);
comment.set('post', null);  //���������ϵ
comment.save();
```
��Ȼ��Ҳ���Դ�һ��һ���Ƴ�������ϵ��
```js
let post = this.store.peekRecord('post', 1);
let comment = this.store.peekRecord('comment', 1);
post.get('comments').removeObject(comment);  // �ӹ����������Ƴ�comment
post.save();
```
��һ��һ��ά����ϵ��ʵ������ά������������Ԫ�ء�
	
ֻҪStore�ı���Handlebarsģ��ͻ��Զ�����ҳ����ʾ�����ݣ��������ʵ���ʱ��Ember Data���Զ����µ��������ϡ�

�й���ģ��֮���ϵ��ά���ͽ��ܵ��������֮���ϵ��ά��ֻ�����ַ�ʽ��һ������һ��һ��ά������һ�����ö��һ��ά���������˵����һ��һ��ά�����򵥡������������Ҫһ���Ը��¶����¼�Ĺ���ʱʹ�õڶ��ַ�ʽ���Ӻ��ʣ�������������������

<br>
���������������[Github](https://github.com/ubuntuvim/my_emberjs_code)�����ľ�������޸ģ������ϵĴ�����github��������г��룬����Ӱ�첻�󣡣����������ò��Ķ����е��ã�����github��Ŀ�ϸ��ҵ��`star`�ɡ����Ŀ϶�������˵�����Ķ�������
