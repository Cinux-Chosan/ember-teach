·�ɵ���һ����Ҫְ������Ⱦͬ���ֵ�ģ�塣

���������·�����ã�`posts`·����Ⱦģ��`posts.hbs`��·��`new`��Ⱦģ��`posts/new.hbs`��
```javascript
Router.map(function() {
     this.route('posts', function() {
     this.route('new');
  });
});
```
ÿһ��ģ�嶼����Ⱦ����ģ���`{{outlet}}`�ϡ����������·������ģ��`posts.hbs`����Ⱦ��ģ��`application.hbs`��`{{outlet}}`�ϡ�`application.hbs`�������Զ���ģ��ĸ�ģ�塣ģ��posts/new.hbs����Ⱦ��ģ��`posts.hbs`��`{{outlet}}`�ϡ�

���������Ⱦ������һ��ģ����Ҳ������ģ�����Ҫ��·������д`renderTemplate`�ص�������
```javascript
//  app/routes/posts.js

import Ember from 'ember';

export default Ember.Route.extend({
	//  ��Ⱦ��favoritesģ����
	renderTemplate: function() {
	    this.render('favorites');
	}
});
```
ģ�����Ⱦ���֪ʶ��Ƚϼ򵥣�����Ҳ���٣���ǰ���[Ember.js ����ָ��֮ʮ�ķ���ƪ��·�ɡ�ģ���ִ�С���Ⱦ˳��](http://blog.ddlisting.com/2016/03/22/ember-js-ru-men-zhi-nan-zhi-shi-si-fan-wai-pian-lu-you-mo-ban-de-zhi-xing-xuan-ran-shun-xu/)�Ѿ����ܹ���ص����ݡ�

<br>
���������������[Github](https://github.com/ubuntuvim/my_emberjs_code)�����ľ�������޸ģ������ϵĴ�����github��������ֳ��룬����Ӱ�첻�󣡣����������ò��Ķ����е��ã�����github��Ŀ�ϸ��ҵ��`star`�ɡ����Ŀ϶�������˵�����Ķ�������
