> Ԫ������������һ���ض���ģʽ�����ͣ�������һ����¼��

һ���ܳ����������Ƿ�ҳ��ͨ����������Ĵ������÷�ҳ��
```js
let result = this.store.query(��post��, {
  limit: 10,
  offset: 0
});
```
������ÿҳ��ʾ����Ϊ10���������㲻֪��������������ô֪��һ���ж���ҳ�أ���ʱ��Ԫ���ݾ������ó��ˡ�
```js
{
  "post": {
    "id": 1,
    "title": "Progressive Enhancement is Dead",
    "comments": ["1", "2"],
    "links": {
      "user": "/people/tomdale"
    },
    // ...
  },

  "meta": {
    "total": 100
  }
}
```
��Щ�����ǴӺ�̨���ص�[JSON](http://www.json.org)��ʽ���ݣ���������ȡԪ���ݿ���ʹ��`this.get('meta')`��ȡ�����������Դ�`query()`�����л�ȡ��

`let` �� `=>` ����[javascript ES6](http://es6.ruanyifeng.com/)���﷨����������˽��й�javascript ES6��Google��

����Ԫ��������Ŀ�е�ʹ�û��ں����������չ�֡��ڽ�����[Ember](http://emberjs.com)����֪ʶ���һ���һ���Ƚ�������С��Ŀ���һ�����Ŀ�о����ܵ�ʹ����������֪ʶ�㣬�����ڴ�����
_С��Ŀ���룺[todos](https://github.com/ubuntuvim/todos_v2)_

<br>
���������������[Github](https://github.com/ubuntuvim/my_emberjs_code)�����ľ�������޸ģ������ϵĴ�����github��������г��룬����Ӱ�첻�󣡣����������ò��Ķ����е��ã�����github��Ŀ�ϸ��ҵ��`star`�ɡ����Ŀ϶�������˵�����Ķ�������
