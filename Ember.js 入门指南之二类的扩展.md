### ��չһ������

> `reopen`��֪����ô����ã��������`reopen`�������Ӧ���ǡ����´򿪡��������ܾ��ò�˳�����Ծ����`��չ`�ˣ�����в�����ָ����

��������չһ���������ֱ��ʹ��`reopen()`����Ϊһ���Ѿ�����õ���������ԡ������������ʹ��`extend()`��������Ҫ���¶���һ�����࣬Ȼ��������������µ����ԡ�������
ǰһƪ����������`create()`����ʱ���ܴ���������Բ��Ҳ��Ƽ��ڴ˷������¶��塢��д����������ʹ��`reopen()`���������ֲ�`create()`�����Ĳ��㡣��`extend()`�����ǳ����ƣ�����Ĵ�����ʾ�����ǵĲ�֮ͬ����

```javascript
Parent = Ember.Object.extend({
    name: 'ubuntuvim',
    fun1() {
        console.log("The name is " + this.name);
    },
    common() {
       console.log("common method..."); 
    }
});   

//  ʹ��extend()��������µ����ԡ�����
Child1 = Parent.extend({
    //  ����ParentΪ����һ������
    pwd: '12345',
    //  ����ParentΪ����һ������
    fun2() {
        console.log("The pwd is " + this.pwd);
    },
    //    ��д�����common()����
    common() {
        //console.log("override common method of parent...");
        this._super();
    }
});
    
var c1 = Child1.create();
console.log("name = " + c1.get('name') + ", pwd = " + c1.get('pwd'));   
c1.fun1();
c1.fun2();     
c1.common();
console.log("-----------------------");    
    
//  ʹ��reopen()��������µ����ԡ�����
Parent.reopen({
    //  ����ParentΪ����һ������
    pwd: '12345',
    //  ����ParentΪ����һ������
    fun2() {
        console.log("The pwd is " + this.pwd);
    },
    //  ��д�౾��common()����
    common() {
        console.log("override common method by reopen method...");
        //this._super();
    },
    //  ����һ����������
    fullName: Ember.computed(function() {
	console.log("compute method...");
    })
});
var p = Parent.create();    
console.log("name = " + p.get('name') + ", pwd = " + p.get('pwd'));   
p.fun1();
p.fun2();    
p.common();
console.log("---------------------------");    
p.get('fullName');  //  ��ȡ��������ֵ��������ֱ�������compute method...

//  ʹ��extend()��������µ����ԡ�����
Child2 = Parent.extend({
    //  ����ParentΪ����һ������
    pwd: '12345',
    //  ����ParentΪ����һ������
    fun2() {
        console.log("The pwd is " + this.pwd);
    },
    //    ��д�����common()����
    common() {
        //console.log("override common method of parent...");
        this._super();
    }
});    
var c2 = Child2.create();
console.log("name = " + c2.get('name') + ", pwd = " + c2.get('pwd'));   
c2.fun1();
c2.fun2(); 
c2.common();
```

![ִ�н��](/content/images/2016/03/19.png)

��ִ�н�����Կ������µĲ���:<br>
**ͬ��**�� ������������չĳ���ࡣ<br>
**���**��<br>
1. `extend`��Ҫ���¶���һ���ಢ��Ҫ�̳б���չ���ࣻ
2. `reopen`���ڱ���չ���౾�����������ԡ�������������չ�������ԣ����`create()`�������� 

�������Ǹ�������ʵ�����������`reopen`������ı���ԭ�����Ϊ����������Ϊ�޸��˶����ԭ�Ͷ���ķ��������ԣ���������ʾʵ��һ����`reopen`����֮����õ�`Child2`���`common`��������Ϊ�Ѿ��ĸı��ˣ��ڱ����������֮ǰ�Ѿ����ù�`reopen`�������п��ܳ����Լ�����֪����ô���µ����⣡
�����`extend`�����ᵼ����Խ��Խ�࣬�̳���Ҳ��Խ��Խ������ܡ�����Ҳ��һ����ս������`extend`����ı䱻�̳������Ϊ��

### ��չ��̬����

ʹ��`reopenClass()`����������չ`static`���͵����ԡ�������

```javascript
Parent = Ember.Object.extend();   
    
//  ʹ��reopenClass()��������µ�static���ԡ�����
Parent.reopenClass({
    isPerson: true,
    username: 'blog.ddlisting.com' 
	//,name: 'test'  //�����е���֣���֪��Ϊ�β���ʹ������Ϊname�������ԣ�����ʾ������Զ����ԣ�ʹ��usernameȴû���⣡������name����������ı����ؼ���
});

Parent.reopen({
    isPerson: false,
    name: 'ubuntuvim'
});
console.log(Parent.isPerson);
console.log(Parent.name);  //  �����
console.log(Parent.create().get('isPerson'));
console.log(Parent.create().get('name'));    //  ��� ubuntuvim
```

������`reopenClass`������ʹ������`name`����������ĵ�ַ�н���

1. [http://discuss.emberjs.com/t/reopenclass-method-can-not-pass-attribute-named-name-of-it/10189](http://discuss.emberjs.com/t/reopenclass-method-can-not-pass-attribute-named-name-of-it/10189)
2. [http://stackoverflow.com/questions/36078464/reopenclass-method-can-not-pass-attribute-named-name-of-it](http://stackoverflow.com/questions/36078464/reopenclass-method-can-not-pass-attribute-named-name-of-it)

���������������[Github](https://github.com/ubuntuvim/my_emberjs_code)�����ľ�������޸ģ������ϵĴ�����github��������ֳ��룬����Ӱ�첻�󣡣����������ò��Ķ����е�����github��Ŀ�ϸ��Ҹ�`star`�ɡ����Ŀ϶�������˵�����Ķ�������