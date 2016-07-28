�����Ӧ��������ʱ��·�����ͻ�ƥ�䵱ǰ��URL���㶨���·���ϡ�Ȼ���ն����·�ɲ������������ݡ�����Ӧ�ó���״̬����Ⱦ·�ɶ�Ӧ��ģ�塣

### 1������·��	

��`app/router.js`��`map`�����ﶨ���·�ɻ�ӳ�䵽��ǰ��URL����`map`���������õ�ʱ�򷽷����ڵ�`route`�����ͻᴴ��·�ɡ�

����ʹ��[Ember CLI](http://ember-cli.com/user-guide)���������·�ɣ�
```
ember generate route about
ember generate route favorites
```
����ִ����֮������������ĿĿ¼`app/routes`���濴���Ѿ������õ�����·���ļ��Ѿ�`app/templates`����·�ɶ�Ӧ��ģ���ļ���
��ʱ��`app/router.js`��`map`�������Ѿ������˸ոմ�����·�����á������[Ember CLI](http://ember-cli.com/user-guide)�Զ�Ϊ�㴴���ˡ�
```javascript
// app/router.js

import Ember from 'ember';
import config from './config/environment';

var Router = Ember.Router.extend({
  location: config.locationType
});

Router.map(function() {
  this.route('about');
  this.route('favorites');
});

export default Router;
```
���ڷֱ��޸�`app/templates`���������ģ���ļ����£�
```html
<!-- app/templates/about.hbs -->

�����aboutģ�壡<br>
{{outlet}}
```
```html
<!-- app/templates/favorites.hbs -->

�����favoritesģ�壡<br>
{{outlet}}
```
Ȼ�����[http://localhost:4200/about](http://localhost:4200/about)����[http://localhost:4200/favorites](http://localhost:4200/favorites)�������ĳ���û��������Ҳ��õ�������ʾ�����

![run result](/content/images/2016/03/55.png)

��������`favorites`���·������̫���Ƿ�����޸ĳ����������أ����ǿ϶��ģ���ֻҪ�޸�`router.js`��`map`���������ü��ɡ�
```javascript
Router.map(function() {
  this.route('about');
  // ע�⣺���ʵ�URL����дfavs������Ŀ�������ʹ��route�ĵط���Ȼ��ʹ��favorites
  this.route('favorites', { path: '/favs' });
});
```
��ʱ���ʣ�[http://localhost:4200/favs](http://localhost:4200/favs)��������ʾ�Ľ����֮ǰ��һ���ġ�

**˵��**��Ĭ������·��ʵ�URL��·��������һ�µģ�����`this.route('about')`��`this.route('about', { path: ��/about�� })`��ͬһ��·�ɣ����URL��·�ɲ�ͬ������Ҫʹ��`{path: '/xxx'}`����ӳ���URL��

��handlebarsģ���п���ʹ��`{{link-to}}`�����ڲ�ͬ��·�ɼ��л���ʹ��ʱ��Ҫ��`link-to`������ָ��·�����ơ���������Ĵ���ʹ��`link-to`����ʵ����`about`��`favs`����·�ɼ��л���
Ϊ��ҳ��������һ������[bootstrap](http://www.bootcss.com/)��ʹ��[npm](https://www.npmjs.com/)���װ��`bower install bootstrap`�������װ�ɹ��������bower_componentsĿ¼�¿���[bootstrap](http://www.bootcss.com/)��ص��ļ�����װ�ɹ�֮�����뵽��Ŀ�У��޸�`chapter3_routes/ember-cli-build.js`����`return`���ǰ�����������д���(���þ�������[bootstrap](http://www.bootcss.com/)���)��
```javascript
app.import("bower_components/bootstrap/dist/css/bootstrap.css");
app.import("bower_components/bootstrap/dist/js/bootstrap.js");
```
�޸�`application.hbs`������һ�������˵���
```html
<!-- //app/templates/application.hbs -->

<nav class="navbar navbar-inverse navbar-fixed-top">
    <div class="container-fluid">
            <div class="navbar-header" href="#">
                <!--  <a class="navbar-brand" href="#">Blog</a> -->
                {{#link-to 'index' class="navbar-brand"}}Home{{/link-to}}
            </div>
            <ul class="nav navbar-nav">
                <li>{{#link-to 'about'}}about{{/link-to}}</li>
       			<li>{{#link-to 'favorites'}}favorites{{/link-to}}</li>
            </ul>
            <ul class="nav navbar-nav navbar-right">
                <li><a href="#">Login</a></li>
                <li><a href="#">Logout</a></li>
            </ul>
    </div>
</nav>

<div class="container-fluid" style="margin-top: 70px;">
<!-- ��Ŀ���������е�ģ�嶼��application����ģ�壬��������ģ�嶼����Ⱦ������� outlet�� -->
{{outlet}}
</div>
```
�������ҳ��û��[bootstrap](http://www.bootcss.com/)Ч��������������Ŀ�����������Ŀ�������������̨�������´���

![run result](/content/images/2016/03/56.png)

���������ͼ������Ҫ��`config/environment.js`�м���һЩ��ȫ�������ô��룬�й����õĽ����뿴������ַ�����½��ܡ�

1. [ember-cli-and-content-security-policy-cs](https://blog.justinbull.ca/ember-cli-and-content-security-policy-csp/)
2. [https://www.w3.org/TR/2015/CR-CSP2-20150721/](https://www.w3.org/TR/2015/CR-CSP2-20150721/)
```javascript
, contentSecurityPolicy: {
      'default-src': "'none'",
      'script-src': "'self' 'unsafe-inline' 'unsafe-eval' use.typekit.net connect.facebook.net maps.googleapis.com maps.gstatic.com",
      'font-src': "'self' data: use.typekit.net",
      'connect-src': "'self'",
      'img-src': "'self' www.facebook.com p.typekit.net",
      'style-src': "'self' 'unsafe-inline' use.typekit.net",
      'frame-src': "s-static.ak.facebook.com static.ak.facebook.com www.facebook.com"
    }
```

![���ý�ͼ](/content/images/2016/03/57.png)

��ͼ���ҵ���ʾ��Ŀ���á�Ȼ����`about`��õ����½���

![result](/content/images/2016/03/58.png)

���Կ����������ַ����URL��Ϊ`about`�ˣ�����ҳ����ʾ������Ҳ��`about`ģ������ݡ�ͬ������`favorites`��ַ���ͱ�Ϊ[http://localhost:4200/favs](http://localhost:4200/favs)������ʾ��������`favorites`�ģ�ΪʲôURL��`favs`������`favorites`�أ���Ϊǰ���Ѿ��޸���`route`��URL��ӳ���ϵ��·��`favorites`��Ӧ��URL��`favs`����
������ʾ�ľ���·�ɵ��л�������

���Կ����������ַ����URL��Ϊabout�ˣ�����ҳ����ʾ������Ҳ��aboutģ������ݡ�ͬ��������favorites����ַ���ͱ�Ϊhttp://localhost:4200/favs������ʾ��������favorites�ģ�ΪʲôURL��favs������favorites�أ���Ϊǰ���Ѿ��޸���route��URL��ӳ���ϵ��·��favorites��Ӧ��URL��favs����
������ʾ�ľ���·�ɵ��л�������

### 2��·��Ƕ��	

���ǵ���ǰ���[Ember.js ����ָ��֮ʮ��{{link-to}} ����](http://blog.ddlisting.com/2016/03/22/ember-js-ru-men-zhi-nan-zhi-shi-san-link-to/)��ƪ���µ�����������ƪ�����бȽ���ϸ�Ľ�����·�ɵ�Ƕ������ôʹ��Ƕ�׵�·�ɡ������ع�ͷȥ���������������Ͳ����ˡ�������в����׵��뿴�����Ľ̡̳�

### 3��application·��

`application`·����Ĭ�ϵ�·�ɣ��ǳ������ڣ����������Զ����·�ɶ��Ƚ���`application`�ŵ��Զ����·�ɡ�����`application`·�ɶ�Ӧ��`application.hbs`ģ���������Զ���ģ��ĸ�ģ�壬�����Զ����ģ�嶼����Ⱦ��application.hbsģ���`{{outlet}}`�ϡ��й���·�ɵ�ִ��˳���Լ�ģ�����Ⱦ˳����ǰ���[Ember.js ����ָ��֮ʮ��{{link-to}} ����](http://blog.ddlisting.com/2016/03/22/ember-js-ru-men-zhi-nan-zhi-shi-san-link-to/)Ҳ�����ˣ��ڴ�Ҳ��������������Ľ����ˡ�����Ի�ͷ��֮ǰ�����»��ߵ������鿴��

### 4��index·��

�������е�Ƕ�׵�·�ɣ���������·��Ember���Զ�����һ������URLΪ`/`��Ӧ·������Ϊ`index`��·�ɡ�

�������������·�������ǵȼ۵ġ�
```javascript
//  app/router.js
// ����

Router.map(function() {
    this.route('about');
    // ע�⣺���ʵ�URL����дfavs������Ŀ�������ʹ��route�ĵط���Ȼ��ʹ��favorites
    this.route('favorites', { path: '/favs' });
});

export default Router;
```

```javascript
//  app/router.js
// ����

Router.map(function() {
	this.route('index', { path: '/' });
    this.route('about');
    // ע�⣺���ʵ�URL����дfavs������Ŀ�������ʹ��route�ĵط���Ȼ��ʹ��favorites
    this.route('favorites', { path: '/favs' });
});

export default Router;
```
`index`·�ɻ���Ⱦ��`application.hbs`ģ���`{{outlet}}`�ϡ������EmberĬ�����á����û�����`/about`ʱEmber���`index`ģ���滻Ϊ`about`ģ�塣

����·��Ƕ�׵����Ҳ����ˡ�
```javascript
//  app/router.js
//  ����
Router.map(function() {

    this.route('posts', function() {
    	this.route('new');
    });

});

export default Router;
```
```javascript
//  app/router.js

//  ����
Router.map(function() {
	this.route('index', { path: '/' });
    this.route('posts', function() {
    	this.route('index', { path: '/' });
    	this.route('new');
    });

});

export default Router;
```
�������÷�ʽ����õ�����ͼ��·�ɱ���������ġ������߹��ߡ��㿪��Ember��ѡ����ڵ㿪��/#Routes����Ϳ��Կ�������·�ɱ���ʾ��˳���п��ܸ���Ĳ�һ������

![·����Ⱦ���](/content/images/2016/03/59.png)

ע��`loading`��`error`������·����ember�Զ����ɵģ����ǵ��÷����ں�������½��ܡ�

���û�����`/posts`ʱʵ�ʽ����·����`posts.index`��Ӧ��ģ����`posts/index.hbs`������ʵ�����Ҳ�û�д������ģ�壬��ΪEmberĬ�ϰ����ģ����Ⱦ��`posts.hbs`��`{{outlet}}`�ϡ��������ģ�岻����Ҳ���൱��ʲô��û������Ȼ��Ҳ���Դ������ģ�塣
<br>ʹ�����`ember generate template posts/index`Ȼ�������ģ�������������ʾ�����ݣ�
```html
<!-- app/templates/posts/index.hbs  -->

<h2>������/posts/index.hbs������</h2>
```
�ٴ˷���[http://localhost:4200/posts](http://localhost:4200/posts)���ǲ��ǿ��Կ������ӵ������ˡ�

�������ô������ÿһ������·�ɵ�·�ɶ���һ����Ϊ`index`����·�ɲ������·�ɶ�Ӧ��ģ��Ϊ`index.hbs`�����������·�ɵ�·�ɵ���һ��ģ�鿴����ô`index.hbs`�������ģ�����ҳ���ر�������һЩ��Ϣϵͳ������Ӧ���Ǻ���Ϥ�ģ�������û����ģ�鶼����һ����ҳ�������ҳ��ʵ�����ݾ���һ�������ģ��ʱ����ʾ�����ݡ���Ȼ����ģ�嵱ȻҲ����������Ҳ����Ⱦ����ģ���`{{outlet}}`�ϡ�������������ӵ��û�����[http://localhost:4200/posts](http://localhost:4200/posts)ʵ�ʽ������[http://localhost:4200/posts/](http://localhost:4200/posts/)���������һ��`/`�����`/`��Ӧ��ģ�����`index`�������û����ʵ���[http://localhost:4200/posts/new](http://localhost:4200/posts/new)����ô����ľ���`posts/new.hbs`���ģ�壨Ҳ����Ⱦ��`posts.hbs`��`{{outlet}}`�ϣ���

### 4����̬�� 

���ڶ�̬����ǰ���[Ember.js ����ָ��֮ʮ��{{link-to}} ����](http://blog.ddlisting.com/2016/03/22/ember-js-ru-men-zhi-nan-zhi-shi-san-link-to/)Ҳ���ܹ��ˣ���������ټ򵥲����¡�

·������Ҫ������֮һ���Ǽ���`model`��

�������·��`this.route('posts');`�������Ŀ�����е�`posts`�µ�`model`�����ǵ���ֻ���������һ��`model`��ʱ����ô�����أ����Ҵ������������ǲ���Ҫһ���Լ�����ȫ�����ݵģ�һ��������Ǽ�������һС���֡����ʱ�����Ҫ��̬���ˣ�

��̬����`:`��ͷ�����Һ������`model`��`id`���ԡ�

```javascript
//  app/router.js

//  ����

Router.map(function() {
    this.route('about');
    // ע�⣺���ʵ�URL����дfavs������Ŀ�������ʹ��route�ĵط���Ȼ��ʹ��favorites
    // this.route('favorites', { path: '/favs' });

    this.route('posts', function() {
    	this.route('post', { path: '/:post_id'});
    });
    
});

export default Router;
```
��ʱ����Է���[http://localhost:4200/posts/1](http://localhost:4200/posts/1)���������ǻ�û����`model`���Իᱨ�����������ʱ���ܣ��������һ���ǽ���`model`�ġ�����ֻҪ֪�������[http://localhost:4200/posts/1](http://localhost:4200/posts/1)���൱�ڻ�ȡ`id`ֵΨһ��`model`��

### 5��ͨ���/ȫ��·��

EmberҲͬ��������ʹ��`*`��ΪURLͨ���������ͨ�����������ö��URL����ͬһ��·�ɡ�
```javascript
this.route('about', { path: '/*wildcard' });
```
Ȼ����ʣ�[http://localhost:4200/wildcard](http://localhost:4200/wildcard)���߷���[http://localhost:4200/2423432ffasdfewildcard](http://localhost:4200/2423432ffasdfewildcard)����[http://localhost:4200/2333](http://localhost:4200/2333)���ǿ��Խ��뵽`about`���·�ɣ�����[http://localhost:4200/posts](http://localhost:4200/posts)��Ȼ�������`posts`���·�ɡ���Ϊ����ƥ�䵽���·�ɡ�

### 6��������·�ɵ������ռ�

����·��Ƕ�׵�����£�һ��������Ƿ���URL�ĸ�ʽ����`��·����/��·����`��Ember�ṩ��һ��`resetNamespace:true`ѡ������û�������·�ɵ������ռ䣬ʹ��������õ�·�ɿ���ֱ����������`/��·����`������Ҫд��·������
```javascript
this.route('posts', function() {
    this.route('post', { path: '/:post_id'});
    this.route('comments', { resetNamespace: true}, function() {
    	this.route('new');
    });
});
```
��ʱ��������ʵ�`new`���·�������ֱ�Ӳ�д`comments`��[http://localhost:4200/posts/new](http://localhost:4200/posts/new)��������Ҫ[http://localhost:4200/posts/comments/new](http://localhost:4200/posts/comments/new)������ģ����Ⱦ��˳��û�䣬`new`ģ����Ȼ����Ⱦ��`comments`��`{{outlet}}`�ϡ�

�������˾��û��ǲ�ʹ��������ñȽϺã��ر����ڿ�����ʱ������Կ������ʵ�URL�Ĳ�Σ�������Դ��뻹�Ǻ��а����ġ�

���ϵ����ݾ��Ƕ���·�ɵ�ȫ�����ݡ����Ƿǳ���Ҫ��֪ʶ��ϣ�����ܺú����գ�����·�ɵ�Ƕ���뿴֮ǰ�����¡������������������Ի��߷��ʹ�����ԭ�̡̳�
<br>
���������������[Github](https://github.com/ubuntuvim/my_emberjs_code)�����ľ�������޸ģ������ϵĴ�����github��������ֳ��룬����Ӱ�첻�󣡣����������ò��Ķ����е��ã�����github��Ŀ�ϸ��ҵ��`star`�ɡ����Ŀ϶�������˵�����Ķ�������
