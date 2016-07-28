[Ember](http://emberjs.com)��[Store](http://emberjs.com/api/data/classes/DS.Store.html)����һ������أ��û��ύ�������Լ��ӷ�������ȡ�����ݻ����ȱ��浽Store������û��ٴ�������ͬ�����ݻ�ֱ�Ӵ�Store�л�ȡ�������Ƿ���HTTP����ȥ��������ȡ��

�����ݷ����仯���������ȸ��µ�Store�У�Store�������µ�����ҳ�档���Ե���ı�Store�е�����ʱ����������Ӧ������������һƪ���¼�¼С�ᣬ�����޸�`article`������ʱ��������Ӧ��ҳ���ϡ�

## 1��push()����

����Ե���`push()`����һ���԰Ѷ������ݱ��浽Store�С���������Ĵ��룺
```js
//  app/routes/application.js

import Ember from 'ember';

export default Ember.Route.extend({
	model: function() {
		this.store.push({
			data: [
				{
					id: 1,
					type: 'album',
					attributes: {   //  ����model����ֵ
						title: 'Fewer Moving Parts',
						artist: 'David Bazan'
						songCount: 10
					},
					relationships: {}  //  ��������model�Ĺ�����ϵ
				},
				{
					id: 2,
					type: 'album',
					attributes: {   //  ����model����ֵ
						title: 'Calgary b/w I Can\'t Make You Love Me/Nick Of Time',
				        artist: 'Bon Iver',
				        songCount: 2
					},	
					relationships: {}  //  ��������model�Ĺ�����ϵ
				}
			]
		});
	}
});
```
**ע��**��`type`����ֵ������ģ�͵��������֡�`attributes`��ϣ�������ֵ��ģ��������Զ�Ӧ��

��ƪ���Ǻ���Ҫ���ͼ���һ�ᣬ������Ȥ�뿴[Pushing Records Into The Store](https://guides.emberjs.com/v2.5.0/models/pushing-records-into-the-store/)����ϸ���ܡ�

<br>
���������������[Github](https://github.com/ubuntuvim/my_emberjs_code)�����ľ�������޸ģ������ϵĴ�����github��������г��룬����Ӱ�첻�󣡣����������ò��Ķ����е��ã�����github��Ŀ�ϸ��ҵ��`star`�ɡ����Ŀ϶�������˵�����Ķ�������

