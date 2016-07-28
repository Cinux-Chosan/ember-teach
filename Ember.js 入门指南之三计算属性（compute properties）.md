### �򵥵ļ�������

�򵥵���˵���������Ծ��ǽ���������Ϊ���ԣ��������ڵ�����һ��������`Ember`���Զ���������������������������ص�������Զ����仯����ʱ�������ݡ�

```javascript
Person = Ember.Object.extend({
    firstName: null,
    lastName: null,
    
    //  fullName ����һ����������
    fullName: Ember.computed('firstName', 'lastName', function() {
        return this.get('firstName') + ", " + this.get('lastName');
    })
});

//  ʵ����ͬʱ�������
var piter = Person.create({
    firstName: 'chen',
    lastName: 'ubuntuvim'
});
console.log(piter.get('fullName'));  // output >>   chen, ubuntuvim
```

����������ʵ����һ�������������Ӵ�����`jQuery��Extjs`������طǳ���Ϥ��������������к���������ô����ġ�ֻ������`Ember`�У������ֺ��������������������ҿ���ͨ��get��ȡ�����ķ���ֵ��

### ����������

��`Ember`�����У��������Ի��ܵ�������һ���������ԣ��γɼ�����������Ҳ����������չĳ������������һʵ���Ļ���������һ��`description()`������

```javascript
Person = Ember.Object.extend({
    firstName: null,
    lastName: null,
    age: null,
    county: null,
    
    //  fullName ����һ����������
    fullName: Ember.computed('firstName', 'lastName', function() {
        return this.get('firstName') + ", " + this.get('lastName');
    }),
    description: Ember.computed('fullName', 'age', 'county', function() {
        return this.get('fullName') + " age " + this.get('age') + " county " + this.get('county');
    })
});

//  ʵ����ͬʱ�������
var piter = Person.create({
    firstName: 'chen',
    lastName: 'ubuntuvim',
    age: 25,
    county: 'china'
});
console.log(piter.get('description'));  // output >>   chen, ubuntuvim
```

���û�ʹ��`set`�����ı�`firstName`��ֵ��Ȼ���ٵ���`get('description')`�õ���ֵҲ�Ǹ��º��ֵ��

### ��д�������Ե�get��set����

ע��Ҫ����д��������Ϊ��������`computed`������Ҫ����������ԵĶ��巽���������ʱ��`computed`���������һ��������һ��`function`������д��ʱ�����һ��������һ��`hash`��

```javascript
//    ��д�������Ե�get��set����
Person = Ember.Object.extend({
    firstName: null,
    lastName: null,
    
    //  ��д��������fullName��get��set����
    fullName: Ember.computed('firstName', 'lastName', {
        get(key) {
            return this.get('firstName') + "," + this.get('lastName');
        },
        set(key, value) {
            //  ����ٷ��ĵ�ʹ�õĴ��룬���������е�ʱ����� Uncaught SyntaxError: Unexpected token [  ������󣬲�֪���Ƿ���ȱ��ĳ���ļ��������Ჹ�ϣ�
//            console.log("value = " + value);
//            var [ firstName, lastName ] = value.split(/\s+/);  
            var firstName = value.split(/\s+/)[0];
            var lastName = value.split(/\s+/)[1];
            this.set('firstName', firstName);
            this.set('lastName', lastName);
            
        }
    }),
//    ������ͨ�������޷���дget��set����
//    firstName: Ember.computed('firstName', {
//        get(key) {
//            return this.get('firstName') + "@@";
//        },
//        set(key, value) {
//            this.set('firstName', value);
//        }
//    })
});
    
var jack = Person.create();    
jack.set('fullName', "james kobe");
console.log(jack.get('firstName'));
console.log(jack.get('lastName'));
```

![���н��](/content/images/2016/03/7.png)

### ��������ֵ��ͳ��

���Ǿ������������������ĳ����������ֵ������ĳ�����������������ģ�������`Ember`��`todos`�����������������һ�δ��롣

```javascript
export default Ember.Controller.extend({
  todos: [
    Ember.Object.create({ isDone: true }),
    Ember.Object.create({ isDone: false }),
    Ember.Object.create({ isDone: true })
  ],
  remaining: Ember.computed('todos.@each.isDone', function() {
    var todos = this.get('todos');
    return todos.filterBy('isDone', false).get('length');
  })
});
```

��������`remaining`��ֵ����������`todos`�������ﻹ�и�֪ʶ�㣺����������`computed()`��������һ��`todos.@each.isDone`�����ļ������������һ���ر�ļ�`@each`�����滹�ῴ�����ر�ļ�`[]`������Ҫע��������ּ�����Ƕ�ײ�����ֻ�ܻ�ȡһ����ε����ԡ�����`todos.@each.foo.name`(��ȡ�������ԣ��������ȵõ�foo�ٻ�ȡ`name`)����`todos.@each.owner.@each.name`(Ƕ��)�����ַ�ʽ���ǲ�����ġ�

������4�����`Ember`���Զ����°󶨵ļ�������ֵ��<br>
1.��`todos`����������һ�������`isDone`����ֵ�����仯��ʱ��
2.��`todos`��������Ԫ�ص�ʱ��
3.��`todos`����ɾ��Ԫ�ص�ʱ��
4.�ڿ�������`todos`���鱻�ı�Ϊ�����������ʱ��

�������������ʾ�Ľ����
```javascript
Task = Ember.Object.extend({
  isDone: false  //  Ĭ��Ϊfalse
}); 

WorkerLists = Ember.Object.extend({
  //  ����һ��Task��������
  lists: [
    Task.create({ isDone: false }),
    Task.create({ isDone: true }),
    Task.create(),
    Task.create({ isDone: true }),
    Task.create({ isDone: true }),
    Task.create({ isDone: true }),
    Task.create({ isDone: false }),
    Task.create({ isDone: true })
  ],

  remaining: Ember.computed('lists.@each.isDone', function() {
    var lists = this.get('lists');
    //  �Ȳ�ѯ����isDoneֵΪfalse�Ķ����ٷ���������
    return lists.filterBy('isDone', false).get('length');
  })
});

// ���´���ʹ�õ���API��鿴��http://emberjs.com/api/classes/Ember.MutableArray.html
var wl = WorkerLists.create();
//  ����isDone����ֵδ���κ��޸�
console.log('1,>> Not complete lenght is ' + wl.get('remaining'));  //  output 3
var lists = wl.get('lists');  //  �õ������ڵ�����

// -----  ��ʾ��һ������� 1. ��todos����������һ�������isDone����ֵ�����仯��ʱ��
//  �޸�����һ��Ԫ�ص�isDone�� ֵ
var item1 = lists.objectAt(3);  //  �õ���4��Ԫ�� objectAt()������EmberΪ�����ṩ��
// console.log('item1 = ' + item1);
item1.set('isDone', false);
console.log('2,>> Not complete lenght is ' + wl.get('remaining'));  //  output 4

//  --------- 2.  ��todos��������Ԫ�ص�ʱ��
lists.pushObject(Task.create({ isDone: false }));  //����һ��isDoneΪfalse�Ķ���
console.log('3,>> Not complete lenght is ' + wl.get('remaining'));  //  output 5

//  --------- 3.  ��todos����ɾ��Ԫ�ص�ʱ��
lists.removeObject(item1);  // ɾ����һ��Ԫ��
console.log('4,>> Not complete lenght is ' + wl.get('remaining'));  //  output 4

//  --------- 4.  �ڿ�������todos���鱻�ı�Ϊ�����������ʱ��
//  ����һ��Controller
TodosController = Ember.Controller.extend({
  // �ڿ������ڶ�������һ��Task��������
  todosInController: [
    Task.create({ isDone: false }),
    Task.create({ isDone: true })
  ],
  //  ʹ�ü���@each.isDone�������õ���filterBy()�������˺�Ķ����isDone����
  remaining: function() {
    //  remaining()�������ص��ǿ������ڵ�����
    return this.get('todosInController').filterBy('isDone', false).get('length');
  }.property('@each.isDone')  //  ָ������������
});
todosController = TodosController.create();
var count = todosController.get('remaining');
console.log('5,>> Not complete lenght is ' + count);  //  output 1
```

![������ʾ�Ľ��](/content/images/2016/03/8.png)

����������У����Ƕ����������ǹ�ע�����ڶ���������ϣ�����ʵ���������ܶ�������ǲ�����ϵ�����ڵ������Ƿ�仯�ˣ����ǰ�����Ԫ����Ϊһ�������������������Ԫ�ظ����ı仯������������Ĵ�������Ĵ���������������Ԫ�صı仯�������Ƕ����`isDone`���Եı仯���������������Կ����������ӣ���������ʹ�ü�`[]`�����`@each`���Ӽ��ı仯Ҳ���Կ������ǵĲ�֮ͬ����

```javascript
Task = Ember.Object.extend({
  isDone: false,  //  Ĭ��Ϊfalse
  name: 'taskName',
  //  Ϊ����ʾ������㣬��дtoString()����
  toString: function() {
    return '[name = '+this.get('name')+', isDone = '+this.get('isDone')+']';
  }
}); 

WorkerLists = Ember.Object.extend({
  //  ����һ��Task��������
  lists: [
    Task.create({ isDone: false, name: 'ibeginner.sinaapp.com' }),
    Task.create({ isDone: true, name: 'i2cao.xyz' }),
    Task.create(),
    Task.create({ isDone: true, name: 'ubuntuvim' }),
    Task.create({ isDone: true , name: '1527254027@qq.com'}),
    Task.create({ isDone: true })
  ],

  index: null,
  indexOfSelectedTodo: Ember.computed('index', 'lists.[]', function() {
    return this.get('lists').objectAt(this.get('index'));
  })
});


var wl = WorkerLists.create();
//  ����isDone����ֵδ���κ��޸�
var index = 1;
wl.set('index', index);
console.log('Get '+wl.get('indexOfSelectedTodo').toString()+' by index ' + index);
```

![������ʾ�Ľ��](/content/images/2016/03/9.png)


`Ember.computed`���������кܶ�ʹ�ü�`[]`ʵ�ֵķ����������봴��һ�����������������ʱ���ر����á������ʹ��`Ember.computed.map`��������ļ������ԡ�

```javascript
const Hamster = Ember.Object.extend({
  chores: null,
  excitingChores: Ember.computed('chores.[]', function() { //����Ember chores��һ������
    return this.get('chores').map(function(chore, index) {
      //return `${index} --> ${chore.toUpperCase()}`;  //  ����ʹ��${}���ʽ�������ڱ��ʽ�ڿ���ֱ�ӵ���js����
      return `${chore}`;  //����Ԫ��ֵ
    });
  })
});

//  Ϊ���鸳ֵ
const hamster = Hamster.create({
  //  ����choresҪ����Hamster����ָ�����������һ��
  chores: ['First Value', 'write more unit tests']
});

console.log(hamster.get('excitingChores'));
hamster.get('chores').pushObject("Add item test");  //add an item to chores array
console.log(hamster.get('excitingChores'));
```

`Ember`���ṩ������һ�ַ�ʽȥ�����������͵ļ������ԡ�

```javascript
const Hamster = Ember.Object.extend({
  chores: null,
  excitingChores: Ember.computed('chores.[]', function() {
    return this.get('chores').map(function(chore, index) {
      //return `${index} --> ${chore.toUpperCase()}`;  //  ����ʹ��${}���ʽ�������ڱ��ʽ�ڿ���ֱ�ӵ���js����
      return `${chore}`;  //����Ԫ��ֵ
    });
  })
});

//  Ϊ���鸳ֵ
const hamster = Hamster.create({
  //  ����choresҪ����Hamster����ָ�����������һ��
  chores: ['First Value', 'write more unit tests']
});

console.log(hamster.get('excitingChores'));
hamster.get('chores').pushObject("Add item test");  //add an item to chores array
console.log(hamster.get('excitingChores'));
```

<br>
���������������[Github](https://github.com/ubuntuvim/my_emberjs_code)�����ľ�������޸ģ������ϵĴ�����github��������ֳ��룬����Ӱ�첻�󣡣����������ò��Ķ����е�����github��Ŀ�ϸ��Ҹ�`star`�ɡ����Ŀ϶�������˵�����Ķ�������

