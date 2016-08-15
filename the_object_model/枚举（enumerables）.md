��`Ember`�У�ö���ǰ�������Ӷ���Ķ��󣬲����ṩ�˷ḻ��API��[Ember.Enumerable API](http://emberjs.com/api/classes/Ember.Enumerable.html)��ȥ��ȡ���������Ӷ���`Ember`��ö�ٶ��ǻ���ԭ����`javascript`����ʵ�ֵģ�`Ember`��չ�����еĺܶ�ӿڡ�
`Ember`�ṩһ����׼���ӿڴ���ö�٣���������������ȫ�ı�ײ����ݴ洢���������޸�Ӧ�ó�������ݷ��ʴ��롣
`Ember`��`Enumerable API`�����ܵ�����`ECMAScript`�淶��Ϊ�˼����������ⲻ���ݣ�`Ember`������ʹ�ñ��������ʵ�����顣

������һЩ��Ҫ�����õ�`API`�б���ע���������еĲ�ͬ��
<table border="1">
  <tr bgcolor="#ccc">
      <td>��׼����</td>
      <td>�ɱ��۲췽��</td>
      <td>˵��</td>
  </tr>
  <tr>
    <td>pop</td>
    <td>popObject</td>
    <td>�ú����Ӵ�������ɾ�����������ظ�ɾ����</td>
  </tr>
  <tr>
    <td>push</td>
    <td>pushObject</td>
    <td>����Ԫ��</td>
  </tr>
 <tr>
    <td>reverse</td>
    <td>reverseObject</td>
    <td>�ߵ�����Ԫ��</td>
  </tr>
<tr>
    <td>shift</td>
    <td>shiftObject</td>
    <td>������ĵ�һ��Ԫ�ش�����ɾ���������ص�һ��Ԫ�ص�ֵ</td>
  </tr>
<tr>
    <td>unshift</td>
    <td>unshiftObject</td>
    <td>��������Ŀ�ͷ���һ�������Ԫ�أ��������µĳ���</td>
  </tr>
</table>

��ϸ�ĵ��뿴��[http://emberjs.com/api/classes/Ember.Enumerable.html](http://emberjs.com/api/classes/Ember.Enumerable.html)

���б����Ҳ�ķ�����`Ember`��д��׼��`JavaScript`�������õģ��������Ĳ�֮ͬ����ʹ����ͨ�ķ�������߲��֣����������鲻�������Ӧ�ó������Զ����£����ᴥ���۲��ߣ�����ʹ��`Ember`��д���ķ�������Դ����۲��ߣ�ֻҪ��������б仯`Ember`�Ϳ��Թ۲쵽�����Ҹ��µ�ģ���ϡ�

## ����API

#### 1�����������

��������Ԫ��ʹ��`forEach`������

```javascript
var arr = ['chen', 'ubuntuvm', '1527254027@qq.com', 'i2cao.xyz', 'ubuntuvim.xyz'];
arr.forEach(function(item, index) {
  console.log(index+1 + ", " +item);
});
```

#### 2����ȡ������βԪ��

```javascript
//  ��ȡͷβ��Ԫ�أ�ֱ�ӵ���Ember��װ�õ�firstObject��lastObject��������
console.log('The firstItem is ' + arr.get('firstObject'));  // output> chen
console.log('The lastItem is ' + arr.get('lastObject'));  //output> ubuntuvim.xyz
```

#### 3��map����

```javascript
//  map������ת�����飬���ҿ����ڻص�����������Լ����߼�
//  map�������½�һ�����飬���ҷ��ر�ת�������Ԫ��
var arrMap = arr.map(function(item) {
  return 'map: ' + item;  //  �����Լ�������Ҫ���߼�����
});
arrMap.forEach(function(item, index) {
  console.log(item);
});
console.log('-----------------------------------------------');
```

#### 4��mapBy����

```javascript
// mapBy ���������ض������Եļ��ϣ�
// ���������Ԫ����һ�������ʱ������Ը��ݶ������������ȡ��Ӧֵ
var obj1 = Ember.Object.create({
  username: '123',
  age: 25
});
 
var obj2 = Ember.Object.create({
  username: 'name',
  age: 35
});
var obj3 = Ember.Object.create({
  username: 'user',
  age: 40
});
 
var obj4 = Ember.Object.create({
  age: 40
});
 
var arrObj = [obj1, obj2, obj3, obj4];  //��������
var tmp = arrObj.mapBy('username');  // 
 
tmp.forEach(function(item, index) {
  console.log(index+1+", "+item);
});
 
console.log('-----------------------------------------------');
```


#### 5��filter����

```javascript
//  filter ������������������ͨ����Ԫ��
//  filter�������Ը���ָ�����������˵���ƥ������ݣ���������Ĵ��룺������Ԫ�ش���4��Ԫ��
var nums = [1, 2, 3, 4, 5];
//  ����selfֵ���鱾��
var numsTmp = nums.filter(function(item, index, self) {
    return item < 4;
});
 
numsTmp.forEach(function(item, index) {
  console.log('item = ' + item);  //  1�� 2�� 3
});
console.log('-----------------------------------------------');
```

`filter`�����᷵�������ж�Ϊ`true`��Ԫ�أ�����жϽ��Ϊ`false`����`undefined`��Ԫ�ع��˵���

#### 6��filterBy����

```javascript
//  ���������ݶ����ĳ�����Թ�����������Ҫ��filterBy��������������Ĵ������isDone����������Թ���
var o1 = Ember.Object.create({
  name: 'u1',
  isDone: true
});
 
var o2 = Ember.Object.create({
  name: 'u2',
  isDone: false
});
 
var o3 = Ember.Object.create({
  name: 'u3',
  isDone: true
});
 
var o4 = Ember.Object.create({
  name: 'u4',
  isDone: true
});
 
var todos = [o1, o2, o3, o4];
var isDoneArr = todos.filterBy('isDone', true);  //���o2���˵�
isDoneArr.forEach(function(item, index) {
  console.log('name = ' + item.get('name') + ', isDone = ' + item.get('isDone'));
  // console.log(item);
});
 
console.log('-----------------------------------------------');
```

`filter`��`filterBy`��ͬ�ĵط���ǰ�߿����Զ�������߼������߿���ֱ��ʹ�á�

#### 7��every��some����

```javascript
// every��some ����
// every �����ж����������Ԫ���Ƿ�����������������Ԫ�ض�����ָ�����ж������򷵻�true�����򷵻�false
// some �����ж����������Ԫ��ֻҪ��һ��Ԫ�ط��������ͷ���true�����򷵻�false
Person = Ember.Object.extend({
  name: null,
  isHappy: true
});
var people = [
  Person.create({ name: 'chen', isHappy: true }),
  Person.create({ name: 'ubuntuvim', isHappy: false }),
  Person.create({ name: 'i2cao.xyz', isHappy: true }),
  Person.create({ name: '123', isHappy: false }),
  Person.create({ name: 'ibeginner.sinaapp.com', isHappy: false })
];
var every = people.every(function(person, index, self) {
  if (person.get('isHappy'))
    return true;
});
console.log('every = ' + every);
 
var some = people.some(function(person, index, self) {
  if (person.get('isHappy'))
    return true;
});
console.log('some = ' + some);
```

#### 8��isEvery��isAny����

```javascript
//  ��every��some���Ƶķ�������isEvery��isAny 
console.log('isEvery = ' + people.isEvery('isHappy', true));  //  ȫ����Ϊtrue�����ؽ������true
console.log('isAny = ' + people.isAny('isHappy', true));  //ֻҪ��һ��Ϊtrue�����ؽ������true
```

����������ʹ������ͨ`JavaScript`�ṩ�ķ�������һ�¡�ѧϰ�ѶȲ��󡭡��Լ������߾Ͷ��ˣ�

��Щ�����ǳ���Ҫ����һ��Ҫѧ�����ʹ�ã�����
<br>
���������������[Github](https://github.com/ubuntuvim/my_emberjs_code)�����ľ�������޸ģ������ϵĴ�����github��������ֳ��룬����Ӱ�첻�󣡣����������ò��Ķ����е�����github��Ŀ�ϸ��Ҹ�`star`�ɡ����Ŀ϶�������˵�����Ķ�������