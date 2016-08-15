>`Ember`���Լ���κ����Եı仯�������������ԡ�

### �۲���ʹ��

`Ember`���Բ���������Եı仯�������������ԡ��۲����Ƿǳ����õģ��ر��Ǽ������԰�֮����Ҫͬ����ʱ��
�۲��߾�����Ember��������ʹ�á�`Ember`��ܱ����Ѿ�����ʹ�ù۲��ߣ����Ƕ��ڴ�����Ŀ�������Կ�������ʱʹ�ü��������Ǹ��ʺϵĽ��������
ʹ�÷�ʽ��������`Ember.observer`����һ������Ϊ�۲��ߡ�

```javascript
// Observer����Emberjs��˵�ǳ���Ҫ��ǰ���㿴���ĺܶ���붼�������й�ϵ����������֮�����ܸ���Ҳ����Ϊ��
Person = Ember.Object.extend({
  firstName: null,
  lastName: null,

  fullName: Ember.computed('firstName', 'lastName', function() {
    return this.get('firstName') + " " + this.get('lastName');
  }),

  //  ��fullName���ı��ʱ�򴥷��۲���
  fullNameChange: Ember.observer('fullName', function() {
    console.log("The fullName is changed by caller");
    //return this.get('fullName');
  })
});

var person = Person.create({
  firstName: 'chen',
  lastName: 'ubuntuvim'
});
// ������۲�ļ������Ի�ûִ�й�get()�������ᴥ���۲���
console.log('fullName = ' + person.get('fullName'));  
//  fullName������firstName��lastName�ģ�����ı���firstName��ֵ���������Ի��Զ����£�
//  fullName���ı������Իᴥ���۲���
person.set('firstName', 'change firstName value');  // �۲��߻ᱻ����
console.log('fullName = ' + person.get('fullName'));
```

`fullName`������`firstName`��`lastName`�ģ�����`set()`�����ı���`firstName`��ֵ����Ȼ�ĵ���`fullName`��ֵҲ���ı��ˣ�`fullName`�仯�˾ʹ����۲��ߡ���ִ�еĽ���Ϳ��Կ�������

![���н��ͼ](/content/images/2016/03/10.png)

`Ember`��Ϊ�������ṩ����һ��ʹ�ù۲��ߵķ�ʽ�����ַ�ʽʹ��������ඨ��֮��Ϊĳ��������������һ���۲��ߡ�

```javascript
person.addObserver('fullName', function() {
    // deal with the change��
});
```

### �۲������첽

Ŀǰ���۲�����`Ember`����ͬ���ģ����Ǳ��󣬹���������ô˵��`Observers in Ember are currently synchronous.`���������ζ��ֻҪ��������һ�����仯�ͻᴥ���۲��ߡ�Ҳ��Ϊ���ԭ������׾ͻ�����������`bug`�ڼ�������û��ͬ����ʱ�򡣱�������Ĵ��룻

```javascript
Person.reopen({
  lastNameChanged: Ember.observer('lastName', function() {
    // The observer depends on lastName and so does fullName. Because observers
    // are synchronous, when this function is called the value of fullName is
    // not updated yet so this will log the old value of fullName
    console.log(this.get('fullName'));
  })
});
```

Ȼ������ͬ����ԭ�������ĵĹ۲���ͬʱ�۲������ԣ��ͻᵼ�¹۲���ִ�ж�Ρ�

```javascript
person = Ember.Object.extend({
  firstName: null,
  lastName: null,

  fullName: Ember.computed('firstName', 'lastName', function() {
    return this.get('firstName') + " " + this.get('lastName');
  }),

  //  ��fullName���ı��ʱ�򴥷��۲���
  fullNameChange: Ember.observer('fullName', function() {
    console.log("The fullName is changed by caller");
    //return this.get('fullName');
  })
});
Person.reopen({
  partOfNameChanged: Ember.observer('firstName', 'lastName', function() {
    //  ͬʱ�۲���firstName��lastName��������
    console.log('========partOfNameChanged======');
  })
});
var person = Person.create({
  firstName: 'chen',
  lastName: 'ubuntuvim'
});

person.set('firstName', '[firstName]');
person.set('lastName', '[lastName]');
```

![run result](/content/images/2016/03/11.png)

��Ȼ��������ִ��������`set()`���Թ۲���Ҳ��ִ��2�Σ����������������Ҫ����ֻ��ִ��һ�ι۲���أ�Ember�ṩ��һ��`once()`�������������������һ��ѭ�����а����Զ�ͬ����ʱ��ִ�С�

```javascript
Person = Ember.Object.extend({
  firstName: null,
  lastName: null,

  fullName: Ember.computed('firstName', 'lastName', function() {
    return this.get('firstName') + " " + this.get('lastName');
  }),

  //  ��fullName���ı��ʱ�򴥷��۲���
  fullNameChange: Ember.observer('fullName', function() {
    console.log("The fullName is changed by caller");
    //return this.get('fullName');
  })
});
Person.reopen({
  partOfNameChanged: Ember.observer('firstName', 'lastName', function() {
    //  ͬʱ�۲���firstName��lastName��������
    //  ����partOfNameChanged�����ǻ�ִ�ж�Σ����Ƿ���processFullNameֻ��ִ��һ��
    console.log('========partOfNameChanged======');  //  
    Ember.run.once(this, 'processFullName');
  }),
  processFullName: Ember.observer('fullName', function() {
    // ����ͬʱ���ö�����Ե�ʱ�򣬴˹۲���ֻ��ִ��һ�Σ������Ƿ�������һ���������Զ���ͬ����ʱ��
    console.log('fullName = ' + this.get('fullName'));
  })
});

var person = Person.create({
  firstName: 'chen',
  lastName: 'ubuntuvim'
});

person.set('firstName', '[firstName]');
person.set('lastName', '[lastName]');
```

![run result](/content/images/2016/03/12.png)

### �۲���������ʼ��

�۲���һֱ�������ʼ�����֮��Ż�ִ�С�
�������۲����ڶ����ʼ����ʱ���ִ�������Ҫ�ֶ�����`Ember.on()`����������������ڶ����ʼ��֮���ִ�С�

```javascript
Person = Ember.Object.extend({
  salutation:null,
  init() {
    this.set('salutation', 'hello');
    console.log('init....');
  },
  salutationDidChange: Ember.on('init', Ember.observer('salutation', function() {
    console.log('salutationDidChange......');
  }))
});

var p = Person.create();
p.get('salutationDidChange');  //  output > init....  salutationDidChange......
console.log(p.get('salutation'));  // output > hello
p.set('salutation');  //  output > salutationDidChange......
```

### δ��ȡ��ֵ�ļ������Բ��ᴥ���۲���

���һ���������Դ���û�е��ù�`get()`������ȡ����ֵ���۲��߾Ͳ��ᱻ��������ʹ�Ǽ������Ե�ֵ�����仯�ˡ��������ô��Ϊ���۲����Ǹ��ݵ���`get()`����ǰ���ֵ�Ƚ��жϳ���������ֵ�Ƿ����ı��ˡ����û���ù�`get()`֮ǰ�ĸı�۲�����Ϊ��û�б仯��
	ͨ�����ǲ���Ҫ������������Ӱ�쵽������룬��Ϊ�������б��۲�ļ��������ڴ���ǰ����ִ��ȡֵ�������������Ȼ���Ĺ۲��߲��ᱻ�������������`init()`������ִ��һ��`get`�������������Ա�֤��Ĺ۲��ڴ���֮ǰ��ִ�й�get�����ġ�
<br>
���ڳ�ѧ����˵������ֵ���Զ����»����е�������⣬����������ô�����·��������ȱ𼱣��ȷ�һ�ţ����Ų�������ѧϰ��ͻ��˽⵽����Ƕ�ôǿ������ԡ�
<br>
���������������[Github](https://github.com/ubuntuvim/my_emberjs_code)�����ľ�������޸ģ������ϵĴ�����github��������ֳ��룬����Ӱ�첻�󣡣����������ò��Ķ����е�����github��Ŀ�ϸ��Ҹ�`star`�ɡ����Ŀ϶�������˵�����Ķ�������


