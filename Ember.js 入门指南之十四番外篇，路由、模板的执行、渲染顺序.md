��Ember��·�ɺ�ģ���ִ�ж�����һ��˳��ģ����ǵ�˳��Ϊ����·��->��·��1->��·��2->��·��3->������ģ����Ⱦ��˳����·��ִ��˳��պ��෴�������һ��ģ�忪ʼ������Ⱦ��

**ע��**��ģ�����Ⱦ��������·��ִ����֮�󣬴����һ��ģ�忪ʼ��������һ������Ĵ������ʾ��֤�������̳��н��ܣ�����鿴��

������һ·�ɸ�ʽΪ`application/posts/detail/comments/comment`����ʱ·��ִ�е�˳��Ϊ��`application/posts` -> `detail` -> `comments` -> `comment`��`application`����ĿĬ�ϵ�·�ɣ��û��Զ��������·�ɶ���`application`����·�ɣ�Ĭ������£������Ӧ��ģ��Ҳ�������������û��Զ����ģ�嶼��`application.hbs`����ģ�塣�����Ҫ�޸�ģ�����Ⱦ����������`route`����д`renderTemplate`�ص��������ں�����ʹ��`render`����ָ��Ҫ��Ⱦ��ģ�壨�磺`render('other')`����Ⱦ��`other`���ģ���ϣ������й���Ϣ��鿴����������Ƕ�Ӧ���ļ�ģ��ṹ����ͼ��

![�ļ�ģ��ṹ](/content/images/2016/03/28.png)

·����ģ�������Ӧ�ģ�����ģ���Ŀ¼�ṹ��·�ɵ�Ŀ¼�ṹ��һ�µġ�
�������ַ�ʽ��������Ŀ¼��

1. �ֶ�����
2. ʹ��������紴��`comment.js`ʹ�����`ember generate route posts/detail/comments/comment`��[Ember CLI](http://ember-cli.com/user-guide/)���Զ�Ϊ���Ǵ���Ŀ¼���ļ���

������Ŀ¼�ṹ֮���������һЩ���뵽ÿ���ļ���������Ŀ֮����ͻ�һĿ��Ȼ�ˡ�����
�����Ұ�ǰ�潲��·��ִ��˳��ֱ��г�ÿ���ļ������ݡ�
```javascript
//  app/routes/posts.js

import Ember from 'ember';

export default Ember.Route.extend({
	model: function() { 
		console.log('running in posts...');
		return { id: 1, routeName: 'The route is posts'};
		// return Ember.$.getJSON('https://api.github.com/repos/emberjs/ember.js/pulls');
	}
	
});
```

```javascript
import Ember from 'ember';

export default Ember.Route.extend({

	model: function(params) {
		console.log('params id = ' + params.post_id);
		console.log('running in detail....');

		return { id: 1, routeName: 'The route is detail..' };
	}
});	
```

```javascript
//  app/routes/posts/detail.js

import Ember from 'ember';

export default Ember.Route.extend({

	model: function(params) {
		console.log('params id = ' + params.post_id);
		console.log('running in detail....');

		return { id: 1, routeName: 'The route is detail..' };
	}
});	
```

```javascript
//  app/routes/posts/detail/comments.js

import Ember from 'ember';

export default Ember.Route.extend({
	model: function() {
		console.log('running in comments...');
		return { id: 1, routName: 'The route is comments....'};
	}
});
```

```javascript
//  app/routes/posts/detail/comments/comment.js

import Ember from 'ember';

export default Ember.Route.extend({
	model: function(params) {
		console.log('params id = ' + params.post_id);
		console.log('running in comment...');
		return { id: 1, routeName: 'The route is comment...'};
	}
});
```
������ģ������ļ������ݡ����г���˳����·�ɵ�˳��һ�¡�
```html
<!--  //  app/templates/posts.hbs  -->

<!-- ���е���·�ɶ�Ӧ��ģ�嶼����Ⱦ��outlet�� -->
{{model.routeName}} >> {{outlet}}
```

```html
<!-- // app/templates/posts/detail.hbs -->

<!-- ���е���·�ɶ�Ӧ��ģ�嶼����Ⱦ��outlet�� -->
{{model.routeName}} >> {{outlet}}
```

```html
<!-- // app/templates/posts/detail/comments.hbs -->

<!-- ���е���·�ɶ�Ӧ��ģ�嶼����Ⱦ��outlet�� -->
{{model.routeName}} >> {{outlet}}
```
```html
<!-- // app/templates/posts/detail/comments/comment.hbs -->

<!-- ���е���·�ɶ�Ӧ��ģ�嶼����Ⱦ��outlet�� -->
{{model.routeName}} >> {{outlet}}
```

��ͼ��·��ִ�е�˳�򣬲�����ִ�еĹ�������Ⱦ·�ɶ�Ӧ��ģ�塣

![·��ִ�е�˳��](/content/images/2016/03/29.png)

����ͼ�п�������Ŀ�����������һ��URLʱ����URL��ص�·������ôִ�еġ�

1. ִ����·�ɣ�Ĭ����`application`������ʱ���뵽·�ɵ�`model`�ص����������ҷ�����һ������`{ id: 1, routeName: 'The route is application...' }`��ִ����ص�֮�����ת����·��ִ��ֱ�����һ��·��ִ����ϣ����е�·��ִ�����֮��ʼ��Ⱦҳ�档
2. ҳ�����Ⱦ���Ǵ����һ��·�ɶ�Ӧ��ģ�忪ʼ������������ĸ�ģ��������Ⱦ��
Ϊ����֤�Ƿ���������ִ��˳�������޸�`detail.js`��
`comments.js`���ڴ����м���һ��ģ�����ߵĲ�����
```javascript
//  app/routes/posts/detail.js

import Ember from 'ember';

export default Ember.Route.extend({

	model: function(params) {
		console.log('params id = ' + params.post_id);
		console.log('running in detail....');

		//  ִ��һ��ѭ����ģ������
		for (var i = 0; i < 10000000000; i++) {
			
		}
		console.log('The comment route executed...');


		return { id: 1, routeName: 'The route is detail..' };
	}
});	
```
```javascript
//  app/routes/posts/detail/comments.js

import Ember from 'ember';

export default Ember.Route.extend({
	model: function(params) {
		console.log('params id = ' + params.post_id);
		console.log('running in comment...'); 
		//  ִ��һ��ѭ����ģ������
		for (var i = 0; i < 10000000000; i++) {
			
		}

		return { id: 1, routeName: 'The route is comment...'};
	}
});
```
ˢ��ҳ�棬ע��鿴����̨�����Ϣ��ҳ����ʾ�����ݡ�
�¿�һ�����ڣ�ִ��URL��[http://localhost:4200/posts/2/comments](http://localhost:4200/posts/2/comments)��

![run result](/content/images/2016/03/30.png)

����̨���������ʱ����ȴ���ִ��`for`ѭ��������ʱ�Ѿ�ִ��������·��`application`��`posts`����������ִ��`detail`������ҳ���ǿհ׵ģ�û���κ�HTMLԪ�ء�

![run result](/content/images/2016/03/31.png)

��`detail`·��ִ�����֮��ת��·��`comments`��Ȼ��ִ�е�`for`ѭ��ģ�����ߣ���ʱҳ����Ȼ��û���κ�HTMLԪ�ء�Ȼ��ȵ�����`route`ִ�����֮�󣬽������ʾ`model`�ص������õ���Ϣ��

![run result](/content/images/2016/03/33.png)

![run result](/content/images/2016/03/32.png)

ÿ����·�����õ���Ϣ������Ⱦ�����һ����·�ɶ�Ӧģ���`{{outlet}}`���档

![run result](/content/images/2016/03/34.png)

1. ��Ⱦ`comment`
�õ�������Ϊ����`comment`��Ⱦ��ɡ�
2. ��Ⱦ`comment`����ĸ�ģ��`comments`
�õ�������Ϊ����`comment`��Ⱦ��� `comments`��Ⱦ��ɡ�
3. ��Ⱦ`comments`����ĸ�ģ��`detail`
�õ�������Ϊ����`comment`��Ⱦ��� `comments`��Ⱦ��� `detail`��Ⱦ��ɡ�
4. ��Ⱦ`detail`����ĸ�ģ��`posts`
�õ�������Ϊ����`comment`��Ⱦ��� `comments`��Ⱦ��� `detail`��Ⱦ��� `posts`��Ⱦ��ɡ�
5. ��Ⱦ`posts`����ĸ�ģ��`application`
�õ�������Ϊ����`comment`��Ⱦ��� `comments`��Ⱦ��� `detail`��Ⱦ��� `posts`��Ⱦ��� `application`��Ⱦ��ɡ�

ֻҪ��סһ�仰��**��ģ��Ķ�����Ⱦ����ģ���`{{outlet}}`�ϣ��������е�ģ�嶼�ᱻ��Ⱦ��`application`��`{{outlet}}`�ϡ�**

<br>
���������������[Github](https://github.com/ubuntuvim/my_emberjs_code)�����ľ�������޸ģ������ϵĴ�����github��������ֳ��룬����Ӱ�첻�󣡣����������ò��Ķ����е��ã�����github��Ŀ�ϸ��ҵ��`star`�ɡ����Ŀ϶�������˵�����Ķ�������
