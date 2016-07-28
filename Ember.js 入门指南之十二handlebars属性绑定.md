�򵥽����԰���ʵ������HTML��ǩ�ڣ�����һ����ǩ�ġ�<���͡�>����ʹ�ã�ֱ��ʹ��`handlebars`���ʽ������ֱ����`handlebars`���ʽ��ֵ��ΪHTML��ǩ��ĳ�����Ե�ֵ��

׼��������
`ember generate route binding-element-attributes`

### 1�����ַ���
```html
<!-- //  app/templates/binding-element-attribute.hbs -->

<div id="logo">
	<img src={{model.imgUrl}} alt='logo' />
</div>
```
�ڶ�Ӧ��`route:binding-element-attributes`�����Ӳ������ݡ�
```javascript
import Ember from 'ember';

export default Ember.Route.extend({
	model: function() {
		return { imgUrl: 'http://i1.tietuku.com/1f73778ea702c725.jpg' };
	}
});
```
����֮��ģ����������´��룺
```html
<div id="logo">
	<img alt="logo" src="http://i1.tietuku.com/1f73778ea702c725.jpg">
</div>
```
���Կ���`{{model.imgUrl}}`�����ַ�������ʽ�󶨵�`src`�����ϡ�

### 2����Booleanֵ
�ڿ������������Ǿ��������ĳ��ֵ�ж��Ƿ��ĳ����ǩ����CSS�࣬���߸���ĳ��ֵ������ť�Ƿ���õȵȡ�����ôember����ô�����أ���
��������Ĵ�����ʾ����`checkbox`��ť���ݰ󶨵�����`isEnable`��ֵ�����Ƿ���á�
```html
{{! ��isEnableΪtrueʱ��disabledΪtrue�������ã��������}}
<input type='checkbox' disabled={{model.isEnable}}>
```
�����`route`�����õ�ֵ��`true`��ô��Ⱦ֮���HTML���£�
```html
<input type="checkbox" disabled="">
```
����
```html
<input type="checkbox">
```

### 3, ��data-xxx����
Ĭ������£�ember����󶨵�`data-xxx`��һ�������ϡ���������İ󶨽���͵ò������Ԥ�ڡ�
```html
{{! �󶨵�data-xxx����������Ҫ��������}}
{{#link-to 'photo' data-toggle='dropdown'}} link-to {{/link-to}}
{{input type='text' data-toggle='tooltip' data-placement='bottom' title="Name"}}
```
ģ����Ⱦ֮��õ������HTML����
```html
<a id="ember455" href="/binding-element-attributes" class="ember-view active"> link-to </a>
<input id="ember470" title="Name" type="text" class="ember-view ember-text-field">
```
���Կ���`data-xxx`�����Զ������ˣ��������ںܶ��ǰ�˿�ܶ����õ�`data-xxx`������ԣ�����`bootstrap`������ô���ء����������view��ָ����Ӧ����Ⱦ���`Ember.LinkComponent`��`Ember.TextField`���������ģ���
ִ������õ�view�ļ���<br>
`ember generate view binding-element-attributes`��<br>
��view���ֶ��󶨣����£�

```javascript
//  app/views/binding-element-attributes.js

import Ember from 'ember';

export default Ember.View.extend({
});

//  �����ǹٷ����Ĵ��룬�������Կ���������ʹ�÷�ʽ����2.0�汾�ģ���
//  2.0�汾��д������ѧϰ�У������ڲ��ϣ�����Ϊ����ʾģ��Ч����ʱ��ôд���Ͼ����ĵ��ص㻹����ģ�����Եİ���

//  ��input
Ember.TextField.reopen({
	attributeBindings: ['data-toggle', 'data-placement']
});

// //  ��link-to
Ember.LinkComponent.reopen({
	attributeBindings: ['data-toggle']
});
```
��Ⱦ֮��õ��Ľ������Ԥ�ڡ��õ�����HTML����
```html
<a id="ember398" href="/binding-element-attributes" data-toggle="dropdown" class="ember-view active">link-to</a>
<input id="ember414" title="Name" type="text" data-toggle="tooltip" data-placement="bottom" class="ember-view ember-text-field">
```

���Կ���`data-xxx`������������Ⱦ��HTML���ˡ�

���Ľ����˼������õ����԰󶨷�ʽ���ǳ�֮ʵ�ã������е��ź������������޻�û��⵽���һ��ʵ����`Ember2.0`��������ôʹ�õģ����ڵĴ����Ǹ��ݸ�������ָ������Ĵ������view���ٷ��̸̳���Ҳ����`Ember2.0`��ģ�����`binding-element-attributes.js`����ļ��Ĵ����е������ˡ���ϣ�������ǲ��ߴͽ̣�
<br>
���������������[Github](https://github.com/ubuntuvim/my_emberjs_code)�����ľ�������޸ģ������ϵĴ�����github��������ֳ��룬����Ӱ�첻�󣡣����������ò��Ķ����е��ã�����github��Ŀ�ϸ��ҵ��`star`�ɡ����Ŀ϶�������˵�����Ķ�������



