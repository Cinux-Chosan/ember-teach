[Ember](http://emberjs.com)�������˴�ƪ��������`model`�����֮ǰ��`controller`��ֱ��������֮�𰡣�

�ӱ�ƪ��ʼѧϰ[Ember](http://emberjs.com)��ģ�ͣ���һ��Ҳ��[Ember](http://emberjs.com)�������ֵ����һ�����ݣ��ǳ�����Ҫ���������Ų��ŷ����������ˣ���

�ڿ�ʼѧϰ`model`֮ǰ������׼��������
���´���һ��[Ember](http://emberjs.com)��Ŀ���Ծ�ʹ�õ���[Ember CLI](http://ember-cli.com/user-guide)�������
```
ember new chapter6_models
cd chapter6_models
ember server
```
�������ִ����Ŀ������������Ϣ˵����Ŀ��ɹ���
**Welcome to Ember**

������ʾ���õ��Ĵ��붼���Դ�[https://github.com/ubuntuvim/my_emberjs_code/tree/master/chapter6_models](https://github.com/ubuntuvim/my_emberjs_code/tree/master/chapter6_models)��ȡ��

�ڽ���`model`֮ǰ������Ŀ������[firebase](https://www.firebase.com/)����ص����ý̲����Ʋ��������޷�����ҳ��������[https://www.firebase.com/](https://www.firebase.com/)ע���û�����firebase�Ĺ����ṩ��ר������Ember�İ汾�����ṩ�˷ǳ��򵥵����ӡ��Ӱ�װ�����϶������˷ǳ���ϸ����̡̳�
�������ҵ����ϲ��裨���������ĿĿ¼��ִ�еģ���

* ��װ
```
ember install emberfire
```
��װ���֮����Զ�����`adapter��app/adapters/application.js��`����������ļ�����Ҫ���κ��޸ģ������ṩ�Ĵ���Ҳ��������Ŀ�Ĵ��벻ͬ��Ӧ���ǹ����İ汾�Ǿɰ�ġ�

* ����`config/environment.js`
�޸ĵڰ���`firebase: 'https://YOUR-FIREBASE-NAME.firebaseio.com/'`�������ַ����ע���û�ʱ��õ��ġ�����Դ�[����](https://www.firebase.com/account/#/)�鿴��ĵ�ַ��������ͼ��ʾλ��

![��ͼ](/content/images/2016/04/134.png)

* ����`config/enviroment.js`��`APP:{}`(��ŵ�20��)�����������´���
```js
APP: {
      // Here you can pass flags/options to your application instance
      // when it is created
    },
    contentSecurityPolicy: {
      'default-src': "'none'",
      'script-src': "'self' 'unsafe-inline' 'unsafe-eval' *",
      'font-src': "'self' *",
      'connect-src': "'self' *",
      'img-src': "'self' *",
      'style-src': "'self' 'unsafe-inline' *",
      'frame-src': "*"
    }
```
Ȼ����ע�͵���7��ԭ�����ԣ���װ`firebase`�Զ����ɵģ��������ò�����������`contentSecurityPolicy`��

��������Բο��ҵ������ļ���
```js
/* jshint node: true */

module.exports = function(environment) {
  var ENV = {
    modulePrefix: 'chapter6-models',
    environment: environment,
    // contentSecurityPolicy: { 'connect-src': "'self' https://auth.firebase.com wss://*.firebaseio.com" },
    firebase: '���firebase����',
    baseURL: '/',
    locationType: 'auto',
    EmberENV: {
      FEATURES: {
        // Here you can enable experimental features on an ember canary build
        // e.g. 'with-controller': true
      }
    },

    APP: {
      // Here you can pass flags/options to your application instance
      // when it is created
    },
    contentSecurityPolicy: {
      'default-src': "'none'",
      'script-src': "'self' 'unsafe-inline' 'unsafe-eval' *",
      'font-src': "'self' *",
      'connect-src': "'self' *",
      'img-src': "'self' *",
      'style-src': "'self' 'unsafe-inline' *",
      'frame-src': "*"
    }
  };

  // ��������ʡ�ԡ���
  return ENV;
};
```
��������������������Ŀ֮�����������ʾһ�ѵĴ�����Ҫ��һЩ����Ȩ�����⡣������֮����Ҫ������Ŀ������Ч��

## 1�����

`model`��һ���������û����ֵײ����ݵĶ��󡣲�ͬ��Ӧ���в�ͬ��`model`����ȡ���ڽ����������Ҫʲô����`model`�Ͷ���ʲô����`model`��
<BR>	
`model`ͨ���ǳ־û��ġ���Ҳ����ζ���û��ر������������`model`���ݲ�Ӧ�ö�ʧ��Ϊ��ȷ��`model`���ݲ���ʧ������Ҫ�洢`model`���ݵ�����ָ���ķ����������Ǳ��������ļ��С�
<BR>
һ�ַǳ�����������ǣ�`model`���ݻ���`JSON`�ĸ�ʽͨ��`HTTP`���͵��������������ڷ����С�Ember��δ�������ṩ��һ�ָ��Ӽ��ķ�ʽ��ʹ��[IndexedDB](w3c.github.io/IndexedDB/)��ʹ����������е����ݿ⣩�����ַ�ʽ�ǰ�`model`���ݱ��浽���ء�����ʹ��[Ember Data](https://github.com/emberjs/data)���ֻ���ʹ��[firebase](https://www.firebase.com/)��������ֱ�ӱ��浽Զ�̷������ϣ������������ҽ�����[firebase](https://www.firebase.com/)�������ݱ��浽Զ�̷������ϡ�
<BR>	
Emberʹ��������ģʽ�������ݿ⣬�������䲻ͬ���͵ĺ�����ݿ������Ҫ�޸��κε�������롣����Դ�[emberobserver](http://emberobserver.com/categories/ember-data-adapters)�Ͽ�����������Ember֧�ֵ����ݿ⡣
<BR>	
�����������EmberӦ�������Զ�̷��������ϣ�����Զ�̷�����`API`���ص����ݲ��ǹ淶��`JSON`����Ҳ��Ҫ����[Ember Data](https://github.com/emberjs/data)���������κη��������ص����ݡ�
<BR>	
[Ember Data](https://github.com/emberjs/data)��֧����ý�������������WebSocket������Դ�һ��socket����Զ�̷���������ȡ���µ����ݻ��߰ѱ仯���������͵�Զ�̷��������档
<BR>	
[Ember Data](https://github.com/emberjs/data)Ϊ���ṩ�˸��Ӽ��ķ�ʽ�������ݣ�ͳһ�������ݵļ��أ����ͳ����Ӷȡ�
<BR>
����`model`��[Ember Data](https://github.com/emberjs/data)�Ľ��ܾ͵���Ϊֹ�ɣ��������˴���ƪ������Model���ڴ��ҾͲ�һһд�����ˣ�̫���ˣ�д����Ҳû�˿��ģ������������Ȥ�Լ����ɣ�[����鿴��ϸ��Ϣ](guides.emberjs.com/v2.0.0/models/#toc_the-store-and-a-single-source-of-truth)��	
<BR>
�����ȿ�һ���򵥵����ӣ����������������й���`model`�ĺ��ĸ����Щ�����Ǿɰ�д����������Ϊ��˵�����⣬����Ҳ��������ִ�С�
```js
//  app/components/list-of-drafts.js
export default Ember.Component.extend({
	willRender() {
		// ECMAScript 6�﷨
		$.getJSON('/drafts').then(data => {
			this.set('drafts', data);
		});
	}
});
```
������һ������ࡣ����������л�ȡ`json`��ʽ���ݡ�
�����������Ӧ��ģ���ļ���
```html
<!-- app/templates/components/list-of-drafts.hbs  -->
<ul>
	{{#each drafts key="id" as |draft|}}
	<li>{{draft.title}}</li>
	{{/each}}
</ul>
```
�ٶ�������һ��������ģ��
```js
//  app/components/list-button.js
export default Ember.Component.extend({
	willRender() {
		// ECMAScript 6�﷨
		$.getJSON('/drafts').then(data => {
			this.set('drafts', data);
		});
	}
});
```
```html
<!-- app/templates/components/ list-button.hbs  -->
{{#link-to ��drafts�� tagName=��button��}}
Drafts ({{drafts.length}})
{{/link-to}}
```
���`list-of-drafts`������`list-button`����һ���ģ��������ǵĶ�Ӧ��ģ��ȴ��һ�������Ƕ��Ǵ�Զ�̷�������ȡͬ�������ݡ����û��`Store`��`model`��������֮һ����ôÿ��������ģ����Ⱦ��������������һ��Զ�����ݡ����ҷ��ص�������һ���ġ��������������˲���Ҫ�����������˲���Ҫ�Ŀ�����û�����Ҳ���á���������`Store`�Ͳ�һ���ˣ�����԰�`Store`���Ϊ�ֿ⣬ÿ��ִ�������ʱ�ȵ�`Store`�л�ȡ���ݣ����û����ȥԶ�̻�ȡ����������һ������иı�ĳЩ���ݣ����ݵĸ���Ҳ����ⷴӦ����һ����ȡ�����ݵ�����ϣ�����������Զ�����һ������������������Ҫ��ȥ����������ܻ�ȡ���¸��Ĺ������ݡ�

��������ݽ�Ϊ��һһ����Ember Data����ĵļ���������`models`��`records`��`adapters`��`store`��

## 2�����ĸ���

��������������ժ����[http://www.emberjs.cn/guides/models/#toc_](http://www.emberjs.cn/guides/models/#toc_)��

#### 1��store

`store`��Ӧ�ô�ż�¼�����Ĳֿ⡣�������Ϊ`store`��Ӧ�õ��������ݵĻ��档Ӧ�õĿ�������·�ɶ����Է�����������`store`����������Ҫ��ʾ�����޸�һ����¼ʱ�����Ⱦ���Ҫ����`store`��

`DS.Store`��ʵ���ᱻ�Զ����������Ҹ�ʵ����Ӧ�������еĶ���������

`store`���Կ�����һ�����档�������`cache`����`store`���ܡ�

��������ӽ��firebase��ʾ��
����·�ɺ�`model`��
```
ember g route store-example
ember g model article
```

```js
//   app/models/article.js

import DS from 'ember-data';

export default DS.Model.extend({
	title: DS.attr('string'),
	body: DS.attr('string'),
	timestamp: DS.attr('number'),
	category: DS.attr('string')
});
```
�������`model`������Ҫ�������ݾ�������Ϊ��û�ж���id�����أ�`Ember`��Ĭ������`id`���ԡ�

������·�ɵ�`model`�ص��л�ȡԶ�̵����ݣ�����ʾ��ģ���ϡ�
```js
//  app/routes/store-example.js

import Ember from 'ember';

export default Ember.Route.extend({
	model: function() {
		// ��store�л�ȡidΪJzySrmbivaSSFG6WwOk�����ݣ���������������ҵ�firebase�г�ʼ���õ�
		return this.store.find('article', '-JzySrmbivaSSFG6WwOk');
	}
});
```
`find`�����ĵ�һ��������`model`�������ڶ������������`id`����ֵ���ǵ�id���Բ���Ҫ��`model`�����ֶ����壬Ember���Զ�Ϊ�㶨�塣
```html
<h1>{{model.title}}</h1>

<div class="body">
{{model.body}}
</div>
```
ҳ�����֮����Կ�����ȡ�������ݡ�

![���صõ�������](/content/images/2016/04/135.png)

�������ҵ�firebase�ϵĲ������ݽ�ͼ��

![firebase����](/content/images/2016/04/136.png)

���Կ����ɹ���ȡ��`id`Ϊ`-JzySrmbivaSSFG6WwOk`�����ݡ�����������ݵĲ����ں������ϸ���ܡ�

#### 2��model

�й�`model`�ĸ���ǰ��ļ���Ѿ������ˣ����ﲻ��׸����
`model`���壺

`model`�������ɸ����Թ��ɵġ�`attr`�����Ĳ���ָ�����Ե����͡�
```js
export default DS.Model.extend({
	title: DS.attr('string'),  //  �ַ�������
	flag: DS.attr('boolean'), //  ��������
	timestamp: DS.attr('number'),  //  ��������
	birth: DS.attr(��date��)  //��������
});
```
ģ��Ҳ������������������Ĺ�ϵ�����磬һ��`Order`���������`LineItems`��һ��`LineItem`��������һ���ض���`Order`��
```js
App.Order = DS.Model.extend({
  lineItems: DS.hasMany('lineItem')
});

App.LineItem = DS.Model.extend({
  order: DS.belongsTo('order')
});
```
��������ݵı�֮��Ĺ�ϵ��һ���ġ�

#### 3��record

`record`��`model`��ʵ���������˴ӷ������˼��ض��������ݡ�Ӧ�ñ���Ҳ���Դ����µļ�¼���Լ����¼�¼���浽�������ˡ�

��¼����������������Ψһ��ʶ��

1. ģ������
2. һ��ȫ��Ψһ��ID

����ǰ���ʵ��`article`����ͨ��`find`����ȡ����ȡ���Ľ������һ��`record`��

#### 4��adapter

��������һ���˽��ض��ķ�������˵Ķ�����Ҫ���𽫶Լ�¼(`record`)������ͱ��ת��Ϊ��ȷ����������˵�������á�

���磬���Ӧ����Ҫһ��`ID`Ϊ`1`��`person`��¼����ôEmber Data����μ������������أ���ͨ��HTTP������Websocket�������ͨ��HTTP����ôURL����`/person/1`������`/resources/people/1`�أ�

�������������������Ƶ����⡣���ۺ�ʱ����Ӧ����Ҫ��`store`�л�ȡһ��û�б�����ļ�¼ʱ��Ӧ�þͻ��������������ȡ�����¼������ı���һ����¼��׼������ı�ʱ��`store`�Ὣ��¼���ݸ���������Ȼ�����������������ݷ��͸��������ˣ���ȷ�ϱ����Ƿ�ɹ���

#### 5��cache

`store`���Զ������¼�����һ����¼�Ѿ��������ˣ���ô�ٴη�������ʱ�򣬻᷵��ͬһ������ʵ������������������������˵�����ͨ�ţ�ʹ��Ӧ�ÿ��Ը����Ϊ�û���Ⱦ�����UI��

���磬Ӧ�õ�һ�δ�`store`�л�ȡһ��`ID`Ϊ`1`��`person`��¼ʱ������ӷ������˻�ȡ��������ݡ�

���ǣ���Ӧ���ٴ���Ҫ`ID`Ϊ`1`��`person`��¼ʱ��`store`�ᷢ�������¼�Ѿ���ȡ���ˣ����һ����˸ü�¼����ô`store`�Ͳ�������������˷�������ȥ��ȡ��¼�����ݣ�����ֱ�ӷ��ص�һ��ʱ���ȡ������������ļ�¼���������ʹ�ò������������¼���ٴΣ����᷵��ͬһ����¼������Ҳ����Ϊ`Identity Map`����ʶ��ӳ�䣩��

ʹ�ñ�ʶ��ӳ��ǳ���Ҫ����Ϊ����ȷ������һ��UI�϶�һ����¼���޸Ļ��Զ�������UI����ʹ�õ��ü�¼��UI��ͬʱ����ζ���������ֶ�ȥ���ֶ����ͬ����ֻ��Ҫʹ��`ID`����ȡӦ���Ѿ���ȡ���ļ�¼�Ϳ����ˡ�

## 3���ܹ����

Ӧ�õ�һ�δ�`store`��ȡһ����¼ʱ��`store`�ᷢ�ֱ��ػ��沢������һ�ݱ�����ļ�¼�ĸ�������ʱ�������������������������ӳ־ò�ȥ��ȡ��¼��ͨ������£��־ò㶼��һ��HTTP����ͨ���÷�����Ի�ȡ����¼��һ��`JSON`��ʾ��

![�ܹ�ͼ1](/content/images/2016/04/137.png)

����ͼ��ʾ����������ʱ����������������ļ�¼����ʱ���������������������һ���첽�����󣬵�������ɼ��غ󣬲���ͨ�����ص����ݴ����ļ�¼��

���ڴ����������첽�ԣ�`store`���`find()`������������һ����ŵ��`promise`�������⣬����������Ҫ`store`�����������������Ļ������᷵�س�ŵ��
һ�������������˵����󷵻ر������¼��JSON����ʱ�������������г�ŵ������`JSON`���ݸ�`store`��
`store`��ʱ�ͻ�ȡ����`JSON`����ʹ��`JSON`������ɼ�¼�ĳ�ʼ������ʹ���¼��صļ�¼�������Ѿ����ص�Ӧ�õĳ�ŵ��

![�ܹ�ͼ2](/content/images/2016/04/138.png)

���潫����һ�µ�`store`�Ѿ�����������ļ�¼ʱ�ᷢ��ʲô��

![�ܹ�ͼ3](/content/images/2016/04/139.png)

�����������£�`store`�Ѿ�����������ļ�¼��������Ҳ������һ����ŵ����ͬ���ǣ������ŵ��������ʹ�û���ļ�¼�����С���ʱ������`store`�Ѿ�����һ�ݿ��������Բ���Ҫ��������ȥ����û���������������������

`models`��`records`��`adapters`��`store`�������Ҫ���ĸ������Ember Data����ĵĶ�����

�й��������ĸ�����ں��������һһ�ô�����ʾ������˱���`model`��һ���µ����ݶ����������ˣ�����
<br>
���������������[Github](https://github.com/ubuntuvim/my_emberjs_code)�����ľ�������޸ģ������ϵĴ�����github��������г��룬����Ӱ�첻�󣡣����������ò��Ķ����е��ã�����github��Ŀ�ϸ��ҵ��`star`�ɡ����Ŀ϶�������˵�����Ķ�������








