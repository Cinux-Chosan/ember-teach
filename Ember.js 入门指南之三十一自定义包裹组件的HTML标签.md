���չ�����������׼��������ʹ��[Ember CLI](http://ember-cli.com/user-guide)����������ʾ������ļ���
```
ember g route customizing-component-element
ember g component customizing-component-element
ember g route home
ember g route about
```
Ĭ������£�����ᱻ������`div`��ǩ�ڡ����磬�����Ⱦ֮��õ�����Ĵ��룺
```html
<div id="ember180" class="ember-view">
  <h1>My Component</h1>
</div>
```
`h1`��ǩ������������ݡ���`ember`��ͷ��`id`��`class`����[Ember](http://emberjs.com)�Զ����ɵġ��������Ҫ�޸���Ⱦ֮�����ɵ�HTML���Ǳ�������`div`��ǩ�������޸�`id`��`class`������ֵΪ�Զ����ֵ�������������������á�

## 1���Զ�����������HTML��ǩ

Ĭ������£�����ᱻ������`div`��ǩ�ڣ��������Ҫ�޸����Ĭ��ֵ��������������ָ�����������HTML��ǩ��
```js
//  app/components/customizing-component-element.js

import Ember from 'ember';

export default Ember.Component.extend({
	// ʹ��tabName����ָ����Ⱦ֮��HTML��ǩ
	// ע�����Ե�ֵ�����Ǳ�׼��HTML��ǩ��
	tagName: 'nav'
});
```
�����Զ���һ�������
```html
<!--  app/templates/components/customizing-component-element.hbs  -->

<ul>
	<li>{{#link-to 'home'}}Home{{/link-to}}</li>
	<li>{{#link-to 'about'}}About{{/link-to}}</li>
</ul>
```
�����ǵ��������ģ����롣ע��������������Ǹ�HTML��ǩ�ڣ���ȷ�����Ӧ���Ǳ�������`nav`��ǩ�С�
```html
<!--  app/templates/customizing-component-element.hbs  -->

{{customizing-component-element}}
```
ҳ�����֮��鿴ҳ���Դ���롣���£�

![���HTML����](/content/images/2016/04/126.png)

���Կ������`customizing-component-element`������ȷʵ�Ǳ�������`nav`��ǩ֮�У�������������û��ʹ������`tagName`ָ��������HTML��ǩ��Ĭ����`div`������԰��������`tagName`����ɾ��֮���ٲ鿴ҳ���HTMLԴ����롣

## 2���Զ�����������HTMLԪ�ص�����

Ĭ������£�[Ember](http://emberjs.com)���Զ�Ϊ���������HTMLԪ������һ����`ember`��ͷ���������������Ҫ�����Զ����CSS�࣬�������������ʹ��`className`��������ָ��������һ����ָ�����CSS�ࡣ��������Ĵ������ӣ�
```js
//  app/components/customizing-component-element.js

import Ember from 'ember';

export default Ember.Component.extend({
	// ʹ��tabName����ָ����Ⱦ֮��HTML��ǩ
	// ע�����Ե�ֵ�����Ǳ�׼��HTML��ǩ��
	tagName: 'nav',
	classNames: ['primary', 'my-class-name']  //ָ������Ԫ�ص�CSS��
});
```
ҳ�����¼���֮��鿴Դ���룬���Կ���`nav`��ǩ�ж�������CSS�࣬һ����`primary`��һ����`my-class-name`��
```html
<nav id="ember411" class="ember-view primary my-class-name">
����
</nav>
```
����������ĳ�����ݵ�ֵ�����Ƿ�����CSS��Ҳ�ǿ��������ģ���������Ĵ��룬��`urgent`Ϊ`true`��ʱ����һ��CSS��`urgent`��������������ࡣҪ�ﵽ���Ŀ�Ŀ���ͨ������`classNameBindings`���á�
```js
//  app/components/customizing-component-element.js

import Ember from 'ember';

export default Ember.Component.extend({
	// ʹ��tabName����ָ����Ⱦ֮��HTML��ǩ
	// ע�����Ե�ֵ�����Ǳ�׼��HTML��ǩ��
	tagName: 'nav',
	classNames: ['primary', 'my-class-name'],  //ָ������Ԫ�ص�CSS��
	classNameBindings: ['urgent'],
	urgent: true
});
```
ҳ�����¼���֮��鿴Դ���룬���Կ���`nav`��ǩ�ж���һ��CSS��`urgent`���������`urgent`��ֵΪ`false`��CSS��`urgent`��������Ⱦ��`nav`��ǩ�ϡ�
```html
<nav id="ember411" class="ember-view primary my-class-name urgent">
����
</nav>
```
**ע��**��`classNameBindings`ָ��������ֵ����Ҫ�������ж����ݵ�������һ�£��������������`classNameBindings`ָ��������ֵ��`urgent`���û��ж��Ƿ������������Ҳ��`urgent`������������ֻ���շ�ʽ��������ô��Ⱦ֮��CSS�����������л���`-`�ָ�������`classNameBindings`ָ��һ����Ϊ`secondClassName`����Ⱦ���CSS��Ϊ`second-class-name`�������������ʾ���룺
```js
//  app/components/customizing-component-element.js

import Ember from 'ember';

export default Ember.Component.extend({
	// ʹ��tabName����ָ����Ⱦ֮��HTML��ǩ
	// ע�����Ե�ֵ�����Ǳ�׼��HTML��ǩ��
	tagName: 'nav',
	classNames: ['primary', 'my-class-name'],  //ָ������Ԫ�ص�CSS��
	classNameBindings: ['urgent', 'secondClassName'],
	urgent: true,
	secondClassName: true
});
```
ҳ�����¼���֮��鿴Դ���룬���Կ���`nav`��ǩ�ж���һ��CSS��`second-class-name`��
```html
<nav id="ember411" class="ember-view primary my-class-name urgent second-class-name">
����
</nav>
```
����㲻����Ⱦ֮���CSS�������޸�Ϊ�л��߷ָ���ʽ�������ֵ`classNameBindings`������ָ����Ⱦ֮���CSS��������������Ĵ��룺
```js
//  app/components/customizing-component-element.js

import Ember from 'ember';

export default Ember.Component.extend({
	// ʹ��tabName����ָ����Ⱦ֮��HTML��ǩ
	// ע�����Ե�ֵ�����Ǳ�׼��HTML��ǩ��
	tagName: 'nav',
	classNames: ['primary', 'my-class-name'],  //ָ������Ԫ�ص�CSS��
	classNameBindings: ['urgent', 'secondClassName:scn'],  //ָ��secondClassName��Ⱦ֮���CSS����Ϊscn
	urgent: true,
	secondClassName: true
});
```
ҳ�����¼���֮��鿴Դ���룬���Կ���`nav`��ǩ��ԭ��CSS��Ϊ`second-class-name`�ı����`scn`��
```html
<nav id="ember411" class="ember-view primary my-class-name urgent scn">
����
</nav>
```
��û�ио�[Ember](http://emberjs.com)�������ǿ�󣡣�[Ember](http://emberjs.com)����������ǡ�Լ���������á������Ժܶ������Ĭ�ϵ����ö�������ƽ����������õĸ�ʽ��
	
������������ָ��CSS����֮�⣬��������`classNameBindings`���Ӽ򵥵��߼����ر����ڴ���һЩ��̬Ч����ʱ�����������Ƿǳ����õġ�
```js
//  app/components/customizing-component-element.js

import Ember from 'ember';

export default Ember.Component.extend({
	// ʹ��tabName����ָ����Ⱦ֮��HTML��ǩ
	// ע�����Ե�ֵ�����Ǳ�׼��HTML��ǩ��
	tagName: 'nav',
	classNames: ['primary', 'my-class-name'],  //ָ������Ԫ�ص�CSS��
	classNameBindings: ['urgent', 'secondClassName:scn', 'isEnabled:enabled:disabled'],
	urgent: true,
	secondClassName: true,
	isEnabled: true  //����������Ϊtrue����enabled������Ⱦ��nav��ǩ�ϣ��������ֵΪfalse��disabled������Ⱦ��nav��ǩ�ϣ���������Ŀ����
});
```
��������ע����˵�ģ�`isEnabled:enabled:disabled`�������Ϊһ����Ŀ���㣬�����`isEnabled`��ֵ��Ⱦ��ͬ��CSS�ൽ`nav`�ϡ�

�����HTML������`isEnabled`Ϊ`true`�����������`isEnabled`Ϊ`false`�����������Լ����ԣ�
```html
<nav id="ember411" class="ember-view primary my-class-name urgent scn enabled">
����
</nav>
```
**ע��**����������жϵ�����ֵ����һ��`Boolean`ֵ����һ���ַ�����ô�õ��Ľ��������Ľ���ǲ�һ���ģ�[Ember](http://emberjs.com)��ֱ�Ӱ�����ַ�����ֵ��ΪCSS������Ⱦ�������ı�ǩ�ϡ���������Ĵ��룺
```js
//  app/components/customizing-component-element.js

import Ember from 'ember';

export default Ember.Component.extend({
	// ʹ��tabName����ָ����Ⱦ֮��HTML��ǩ
	// ע�����Ե�ֵ�����Ǳ�׼��HTML��ǩ��
	tagName: 'nav',
	classNames: ['primary', 'my-class-name'],  //ָ������Ԫ�ص�CSS��
	classNameBindings: ['urgent', 'secondClassName:scn', 'isEnabled:enabled:disabled', 'stringValue'],
	urgent: true,
	secondClassName: true,
	isEnabled: true,  //����������Ϊtrue����enabled������Ⱦ��nav��ǩ�ϣ��������ֵΪfalse��disabled������Ⱦ��nav��ǩ�ϣ���������Ŀ����
	stringValue: 'renderedClassName'
});
```
��ʱҳ���HTMLԴ����е㲻һ���ˡ�`renderedClassName`��ΪCSS��������Ⱦ����`nav`��ǩ�ϡ�
```html
<nav id="ember411" class="ember-view primary my-class-name urgent scn enabled renderedClassName">
����
</nav>
```
���������Ҫ�ر�ע�⡣[Ember](http://emberjs.com)����`Boolean`ֵ������ֵ���жϽ���ǲ�һ���ġ�

## 3���Զ�����������HTMLԪ�ص�����
	
��ǰ����������˰��������HTMLԪ�صı�ǩ����CSS��������HTML��ǩ�ϳ���CSS������һ����õľ������ԣ���ô[Ember](http://emberjs.com)ͬ���ṩ���Զ������HTMLԪ�ص����Եķ�����ʹ��`attributeBindings`����ָ����������Ե����Է�ʽ��`classNameBindings`����һ�¡�
Ϊ����ǰ������������½�һ�����`link-items`��ʹ������`ember g component link-items`������
```html
<!--  app/templates/components/link-items.hbs  -->

���Ǹ����
```
��ģ���е��������
```html
<!--  app/templates/customizing-component-element.hbs  -->

{{customizing-component-element}}
<br><br>

{{link-items}}
```
������������ָ࣬��������HTML��ǩΪ`a`��ǩ��������һ������`href`��
```js
//  app/components/link-items.js

import Ember from 'ember';

export default Ember.Component.extend({
	tagName: 'a',
	attributeBindings: ['href'],
	href: 'http://www.google.com.hk'
});
```
ҳ�����¼���֮��õ����½����

![��Ⱦ���HTML����](/content/images/2016/04/127-1.png)

�Ƚϼ򵥣�������Ⱦ֮��Ľ���ҾͲ���������ˣ���ο�`classNameBindings`������⡣

���ˣ��й��������Ⱦ֮����������HTML��ǩ��������ý�����ϡ����ݲ��࣬`classNameBindings`��`attributeBindings`���������Ե�ʹ�÷�ʽ������ͬ���������ʻ�ӭ�������Ի���ֱ�Ӳ鿴�ٷ��̡̳�
<br>
<br>
���������������[Github](https://github.com/ubuntuvim/my_emberjs_code)�����ľ�������޸ģ������ϵĴ�����github��������г��룬����Ӱ�첻�󣡣����������ò��Ķ����е��ã�����github��Ŀ�ϸ��ҵ��`star`�ɡ����Ŀ϶�������˵�����Ķ�������








