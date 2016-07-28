��[Ember](http://emberjs.com)Ӧ���У����л������ʽ�����̨���������ݣ��������ͺͽ��յ����ݡ�Ĭ������»�ʹ��[JSON API](http://jsonapi.org/)���л����ݡ������ĺ��ʹ�ò�ͬ�ĸ�ʽ��Ember Data�������Զ������л������߶���һ����ȫ��ͬ�����л�����

Ember Data�������������л�����[JSONAPISerializer](http://emberjs.com/api/data/classes/DS.JSONAPISerializer.html)��Ĭ�ϵ����л��������봦���˵�JSON API��[JSONSerializer](http://emberjs.com/api/data/classes/DS.JSONSerializer.html)��һ���򵥵����л��������봦����JSON��������Ǵ����¼���顣[RESTSerializer](http://emberjs.com/api/data/classes/DS.RESTSerializer.html)��һ�����ӵ����л�����֧�ֲ�����أ���Ember Data2.0֮ǰ��Ĭ�ϵ����л�����

## JSONAPISerializer�淶

�������������������ʱ��JSONSerializer��ѷ��������ص����ݵ����Ƿ������й淶��JSON���ݡ�

**ע��**���ر�����Ŀʹ�õ����Զ�����������ʱ�򣬺�̨���ص����ݸ�ʽ�������[JSOP API](http://www.jsonapi.org)�淶�������޷�ʵ�����ݵ�CRUD������Ember���޷��������ݣ������Զ�������������֪ʶ�뿴��һƪ[Ember.js ����ָ��֮��ʮ���Զ���������](http://blog.ddlisting.com/2016/04/17/zi-ding-yi-gua-pei-qi/)��������������ϸ�Ľ����Զ������������Զ������л�����ϢϢ��صġ�

#### 1��JSON API�ĵ�

JSONSerializer�ڴ���̨���ص���һ������JSON API�淶��Լ����JSON�ĵ������������JSON���ݣ���Щ���ݵĸ�ʽ�������ģ�

1. typeָ��model������
2. ��������ʹ���л��߷ָ�

��������`/people/123`����Ӧ���������£�
```js
{
  "data": {
    "type": "people",
    "id": "123",
    "attributes": {
      "first-name": "Jeff",
      "last-name": "Atwood"
    }
  }
}
```
�����Ӧ�������ж�������ô`data`������������ʽ���ء�
```js
{
  "data": [
  	{
	    "type": "people",
	    "id": "123",
	    "attributes": {
	      "first-name": "Jeff",
	      "last-name": "Atwood"
	    }
	},{
	    "type": "people",
	    "id": "124",
	    "attributes": {
	      "first-name": "chen",
	      "last-name": "ubuntuvim"
	    }
	}
  ]
}
```
#### 2����������

������ʱ�򲢲�����������壬������������ӡ����ӵĹ�ϵ�����`included`���档
```js
{
  "data": {
    "type": "articles",
    "id": "1",
    "attributes": {
      "title": "JSON API paints my bikeshed!"
    },
    "links": {
      "self": "http://example.com/articles/1"
    },
    "relationships": {
      "comments": {
        "data": [
          { "type": "comments", "id": "5" },
          { "type": "comments", "id": "12" }
        ]
      }
    }
  }],
  "included": [{
    "type": "comments",
    "id": "5",
    "attributes": {
      "body": "First!"
    },
    "links": {
      "self": "http://example.com/comments/5"
    }
  }, {
    "type": "comments",
    "id": "12",
    "attributes": {
      "body": "I like XML better"
    },
    "links": {
      "self": "http://example.com/comments/12"
    }
  }]
}
```
��JSON���ݿ�����`id`Ϊ`5`��`comment`������`"self": http://example.com/comments/5`��`id`Ϊ`12`��`comment`������`"self": http://example.com/comments/12`��������Щ�����ǵ�������`included`�ڡ�

#### 3���Զ������л���

Ember DataĬ�ϵ����л�����JSONAPISerializer��������Ҳ�����Զ������л�������Ĭ�ϵ����л�����

Ҫ�Զ������л�������Ҫ����һ����Ϊ`application`���л�����Ϊ��ڡ�

ֱ��ʹ���������ɣ�`ember g serializer application`
```js
//  app/serializers/application.js

import DS from 'ember-data';

export default DS.JSONSerializer.extend({

});
```
�����㻹�������ĳ��ģ�Ͷ������л�������������Ĵ���Ϊ`post`������һ��ר�ŵ����л�������ǰһƪ�Զ����������н��ܹ����Ϊһ��ģ���Զ����������������������صġ�
```js
//  app/serializers/post.js
import DS from ��ember-data��;
export default DS.JSONSerializer.extend({
});
```
�������ı䷢�͵���˵�JSON���ݸ�ʽ����ֻ����д`serialize`�ص����ڻص����������ݸ�ʽ��

����ǰ�˷��͵����ݸ�ʽ�����½ṹ�� 
```js
{
  "data": {
    "attributes": {
      "id": "1",
      "name": "My Product",
      "amount": 100,
      "currency": "SEK"
    },
    "type": "product"
  }
}
```
���Ƿ��������ܵ����ݽṹ���������ֽṹ��
```js
{
  "data": {
    "attributes": {
      "id": "1",
      "name": "My Product",
      "cost": {
        "amount": 100,
        "currency": "SEK"
      }
    },
    "type": "product"
  }
}
```
��ʱ�������д`serialize`�ص���
```js
//  app/serializers/application.js

import DS from 'ember-data';

export default DS.JSONSerializer.extend({
	serialize: function(snapshot, options) {
		var json = this._super(...arguments);  // ??
		json.data.attributes.cost = {
			amount: json.data.attributes.amount,
			currency: json.data.attributes.currency
		};

		delete json.data.attributes.amount;
		delete json.data.attributes.currency;

		return json;
	}
});
```
��ô����Ƿ������ء�
�����˷��ص����ݸ�ʽΪ��
```js
{
  "data": {
    "attributes": {
      "id": "1",
      "name": "My Product",
      "cost": {
        "amount": 100,
        "currency": "SEK"
      }
    },
    "type": "product"
  }
}
```
����ǰ����Ҫ�ĸ�ʽ�ǣ�
```js
{
  "data": {
    "attributes": {
      "id": "1",
      "name": "My Product",
      "amount": 100,
      "currency": "SEK"
    },
    "type": "product"
  }
}
```
��ʱ�������д�ص�����`normalizeResponse`��`normalize`���ڷ������������ݸ�ʽ��
```js
//  app/serializers/application.js

import DS from 'ember-data';

export default DS.JSONSerializer.extend({

	normalizeResponse: function(store, primaryModelClass, payload, id, requestType) {
		payload.data.attributes.amount = payload.data.attributes.cost.amount;
		payload.data.attributes.currency = payload.data.attributes.cost.currency;

		delete payload.data.attributes.cost;

		return this._super(...arguments);
	}
});
```
####4������ID����

ÿһ�����ݶ���һ��Ψһֵ��Ϊ`ID`��Ĭ�������Ember��Ϊÿ��ģ�ͼ���һ����Ϊ`id`�����ԡ���������Ϊ�������ƣ�����������л�����ָ����
```js
//  app/serializers/application.js

import DS from 'ember-data';

export default DS.JSONSerializer.extend({
	primatyKey: '__id'
});
```
�������������޸�Ϊ`__id`��

#### 5��������

Ember DataԼ�������������շ�ʽ��������ʽ���������л���ȴ���������л��߷ָ���������ʽ������Ember���Զ�ת��������Ҫ�������ֶ�ָ����Ȼ������������޸�����Ĭ�ϵķ�ʽҲ�ǿ��Եģ�ֻ�������л�����ʹ������`keyForAttributes`ָ����ϲ���ķָ���ʽ���ɡ���������Ĵ�������кŵ��������Ƹ�Ϊ���»��߷ָ���
```js
//  app/serializers/application.js

import DS from 'ember-data';

export default DS.JSONSerializer.extend({
  keyForAttributes: function(attr) {
    return Ember.String.underscore(attr);  
  }
});
```

#### 6��ָ���������ı���

�������ģ�����ݱ����л��������л�ʱָ��ģ�����Եı�����ֱ�������л�����ʹ��`attrs`����ָ�����ɡ�
```js
//  app/models/person.js
export default DS.Model.extend({
  lastName: DS.attr(��string��)
});
```
ָ�����л��������л����Ա�����
```js
//  app/serializers/application.js

import DS from 'ember-data';

export default DS.JSONSerializer.extend({
  attrs: {
    lastName: ��lastNameOfPerson��
  }
});
```
ָ��ģ�����Ա���Ϊ`lastNameOfPerson`��

#### 7��ģ��֮��Ĺ�����ϵ

һ��ģ��ͨ��`ID`������һ��ģ�͡�����������ģ�ʹ���һ�Զ��ϵ��
```js
//  app/models/post.js
export default DS.Model.extend({
  comments: DS.hasMany(��comment��, { async: true });
});
```
���л���JSON���ݸ�ʽ���£����й�����ϵͨ��һ�����`ID`����ֵ������ʵ�֡�
```js
{
  "data": {
    "type": "posts",
    "id": "1",
    "relationships": {
      "comments": {
        "data": [
          { "type": "comments", "id": "5" },
          { "type": "comments", "id": "12" }
        ]
      }
    }
  }
}
```
�ɼ���������`comment`������һ��`post`�ϡ�
�����`belongsTo`��ϵ�ģ�JSON�ṹ��`hadMany`��ϵ����
```js
{
  "data": {
    "type": "comment",
    "id": "1",
    "relationships": {
      "original-post": {
        "data": { "type": "post", "id": "5" },
      }
    }
  }
}
```
`id`Ϊ`1`��`comment`������`ID`Ϊ`5`��`post`��

#### 8���Զ���ת������

��ĳЩ����£�Ember���õ��������ͣ�`string`��`number`��`boolean`��`date`�����ǲ����õġ����磬���������ص��ǷǱ�׼�����ݸ�ʽʱ��

Ember Data����ע���µ�JSONת����ȥ��ʽ�����ݣ�����ֱ��ʹ���������`ember g transform coordinate-point`
```js
//  app/transforms/coordinate-point.js

import DS from 'ember-data';

export default DS.Transform.extend({
  deserialize: function(v) {
    return [v.get('x'), v.get('y')];
  },

  serialize: function(v) {
    return Ember.create({ x: v[0], y: v[1]});
  }
});
```
����һ�������������ͣ�����������������Թ��ɣ��γ�һ�����ꡣ
```js
//  app/models/curor.js
import DS from 'ember-data';
export default DS.Model.extend({
  position: DS.attr(��coordinate-point��)
});
```
�Զ������������ʹ�÷�ʽ����ͨ����һ�£�ֱ����Ϊ`attr`�����Ĳ�����������ǽ��ܵ����񷵻ص�������������Ĵ�����ʾ��
```js
{
  cursor: {
    position: [4, 9]
  }
}
```
����ģ��ʵ��ʱ��Ȼ��Ϊһ����ͨ������ء���Ȼ����ʹ��`.`������ȡ����ֵ��
```js
var cursor = this.store.findRecord(��cursor��, 1);
cursor.get(��position.x��);  //  => 4
cursor.get(��position.y��);  //  => 9
```
#### 9��JSONSerializer

���������е�API����ѭJSONAPISerializerԼ��ͨ�����������ռ�Ϳ�����ϵ��¼������ϵͳ�������⣬ԭ�ȵ�API���ص�ֻ�Ǽ򵥵�JSON��ʽ������JSONAPISerializerԼ���ĸ�ʽ����ʱ������Զ������л���ȥ����ɽӿڡ����ҿ���ͬʱ����ʹ��RESTAdapterȥ���к���Щ�򵥵�JSON���ݡ�
```js
//  app/serializer/application.js

export default DS.JSONSerializer.extend({
  // ...
});
```
#### 10��EMBEDDEDRECORDMIXIN

����Ember Data�����㿽��ģ�͹�����ϵ������ʱ���ڴ�������APIʱ����ᷢ������Ҫ�����JSON��Ƕ��������ģ�͵Ĺ�����ϵ������`EmbeddedRecordsMixin`���԰�����������⡣

����`post`�а�����һ��`author`��¼��
```js
{
    "id": "1",
    "title": "Rails is omakase",
    "tag": "rails",
    "authors": [
        {
            "id": "2",
            "name": "Steve"
        }
    ]
}
```
����Զ������ģ�͹�����ϵ���£�
```js
//  app/serializers/post.js
export default DS.JSONSerialier.extend(DS.EmbeddedRecordsMixin, {
  attrs: {
author: {
  serialize: ��records��,
  deserialize: ��records��
}
  }
});
```
����㷢����������Ҫ���л��뷴���л�Ƕ��Ĺ�ϵ�������ʹ������`embedded`���á�
```js
//  app/serializers/post.js
export default DS.JSONSerialier.extend(DS.EmbeddedRecordsMixin, {
  attrs: {
author: { embedded: ��always�� }
  }
});
```
���л��뷴���л�������3���ؼ��֣�

1. `records`  ���ڱ��ȫ���ļ�¼�������л��뷴���л���
2. `ids`  ���ڱ�ǽ������л��뷴���л���¼��id
3. `false`  ���ڱ�Ǽ�¼����Ҫ���л��뷴���л�

���磬����ܻᷢ�������һ��Ƕ��ʽ��¼��ȡʱһ��JSON��Ч�غ�ֻ������ϵ����������л���¼���������ʹ��`serialize: ids`����Ҳ����ѡ��ͨ���������л��Ĺ�ϵ `serialize: false`��
```js
export default DS.JSONSerializer.extend(DS.EmbeddedRecordsMixin, {
  attrs: {
    author: {
      serialize: false,
      deserialize: 'records'
    },
    comments: {
      deserialize: 'records',
      serialize: 'ids'
    }
  }
});
```
#### 11��EMBEDDEDRECORDSMIXIN Ĭ������

�����û����д`attrs`ȥָ��ģ�͵Ĺ�����ϵ����ô`EmbeddedRecordsMixin`�������µ�Ĭ����Ϊ��
```
belongsTo��{serialize: ��id��, deserialize: ��id�� }
hasMany: { serialize: false, deserialize: ��ids�� }
```

#### 12���������л���

�����Ŀ��Ҫ�Զ������л�����Ember�Ƽ���չJSONAIPSerializer����JSONSerializer��ʵ��������󡣵��ǣ����������ȫ����һ��ȫ�µ���JSONAIPSerializer��JSONSerializer����һ�������л����������չ`DS.Serializer`�࣬���������Ҫʵ����������������

1. normalizeResponse
2. serialize
3. normalize

֪���淶��JSON���ݶ�Ember Data��˵�Ƿǳ���Ҫ�ģ����ģ��������������Ember Data�淶��Щ����ֵ�������Զ����¡�������ص�����û����ģ����ָ����ô��Щ���ݽ��ᱻ���ԡ����������ģ�Ͷ��壬`this.store.push()`�������ܵĸ�ʽΪ�ڶ��δ�����ʾ��
```js
//   app/models/post.js
import DS from 'ember-data';
export default DS.Model.extend({
  title: DS.attr(��string��),
  tag: DS.attr(��string��),
  comments: hasMany(��comment��, { async: true }),
  relatedPosts: hasMany(��post��)
});
```
```js
{
  data: {
    id: "1",
    type: 'post',
    attributes: {
      title: "Rails is omakase",
      tag: "rails",
    },
    relationships: {
      comments: {
        data: [{ id: "1", type: 'comment' },
               { id: "2", type: 'comment' }],
      },
      relatedPosts: {
        data: {
          related: "/api/v1/posts/1/related-posts/"
        }
      }
    }
}
```
ÿ�����л���¼���밴�������ʽҪ��ȷ��ת����Ember Data��¼��
<br>
��ƪ�������ѶȺܴ����ڸ߼���������ݣ������ʱ��ⲻ����Ҫ�����������ʹ��[firebase](http://www.firebase.com)������Ŀ��������Ϥ������Ember�����Լ���������ν���֮���ٻع�ͷ����ƪ����һƪ[Ember.js ����ָ��֮��ʮ���Զ���������](http://blog.ddlisting.com/2016/04/17/zi-ding-yi-gua-pei-qi/)�������Ͳ�������������ˣ���
<br>
����ƪΪֹ���й�Ember�Ļ���֪ʶȫ��������ϣ�������2015-08-26��ʼ�����ڸպ�2���£�ԭ�ƻ�����3����ʱ����ɵģ���ǰ��һ���£�����ԭ���Ǻ���������Ѷȴ����ƫ�����������Ҳ���ã��о�ʱ��Ƚϲִ٣�˵�Խ�ʡ�˺ܶ�ʱ�䣡��_��ƪ������������ģ�ԭʼ�沩�ķ�����ʱ��Ember����2.0�汾�������Ѿ���2.5�ˣ���_��
<br>
�������������APPLICATION CONCERNS��TESTING�����£�Ҳ�п��ܰѾɰ��Ember todomvc�����ĳ�Ember2.0�汾�ģ����ÿ��������������٣����� 
<br>
�����ҵ���Ŀ�꣺�Ѿɰ��Ember todomvc�����ĳ�Ember2.0�汾�ģ�Ҳ����ˣ�����������չ�˺ܶ๦�ܣ��йش������[todos v2](https://github.com/ubuntuvim/todos_v2)����ӭ����forkѧϰ������������þ͸���һ��`star`�ɣ���лл������

<br>
���������������[Github](https://github.com/ubuntuvim/my_emberjs_code)�����ľ�������޸ģ������ϵĴ�����github��������г��룬����Ӱ�첻�󣡣����������ò��Ķ����е��ã�����github��Ŀ�ϸ��ҵ��`star`�ɡ����Ŀ϶�������˵�����Ķ�������
