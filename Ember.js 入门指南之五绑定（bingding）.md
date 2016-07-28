���������Ŀ��һ����`Ember`Ҳ�������е����ݰ󶨷�ʽ�����ҿ������κ�һ��������ʹ�ð󶨡���Ȼ�����ݰ󶨴�����������ʹ����`Ember`��ܱ������ڿ�������û���ʹ�ü������Ը�Ϊ�򵥷��㡣

### ˫���

```javascript
// ˫���
Wife = Ember.Object.extend({
  householdIncome: 800
});
var wife = Wife.create();

Hasband = Ember.Object.extend({
  //  ʹ�� alias����ʵ�ְ�
  householdIncome: Ember.computed.alias('wife.householdIncome')
});

hasband = Hasband.create({
  wife: wife
});

console.log('householdIncome = ' + hasband.get('householdIncome'));  //  output > 800
// ����˫������ֵ

//  ��wife������ֵ
wife.set('householdIncome', 1000);
console.log('householdIncome = ' + hasband.get('householdIncome'));  // output > 1000
// ��hasband������ֵ
hasband.set('householdIncome', 10);
console.log('wife householdIncome = ' + wife.get('householdIncome'));
```

![run result](/content/images/2016/03/13.png)

��Ҫע����ǰ󶨲��������̸��¶�Ӧ��ֵ��`Ember`��ȴ�ֱ������������������ɲ�������ͬ���ı�֮ǰ����������Զ�θı�������Ե�ֵ�����ڰ��Ǻܶ��ݵ�����Ҳ����Ҫ���Ŀ������⡣

### �����

�����ֻ����һ�������ϴ����仯�����˫�����˵����������������Ż�������˫�����˵�����ֻ����һ�����������ù�����ʵ����һ������󶨡�

```javascript
var user = Ember.Object.create({
  fullName: 'Kara Gates'
});

UserComponent = Ember.Component.extend({
  userName: Ember.computed.oneWay('user.fullName')
});

userComponent = UserComponent.create({
  user: user
});

console.log('fullName = ' + user.get('fullName'));
// ��user��������
user.set('fullName', "krang Gates");
console.log('component>> ' + userComponent.get('userName'));
// UserComponent ����ֵ��user�����ܻ�ȡ����Ϊ�ǵ���İ�
userComponent.set('fullName', "ubuntuvim");
console.log('user >>> ' + user.get('fullName'));
```

![run result](/content/images/2016/03/14.png)

�������ݰ󶨵�֪ʶ�㲻�࣬�����˵�����ص㣬�Ͼ�����֮��Ĺ�����ϵ��Խ�١�Խ��Խ�á�������ϵ���˷�������ά����
<br>
���������������[Github](https://github.com/ubuntuvim/my_emberjs_code)�����ľ�������޸ģ������ϵĴ�����github��������ֳ��룬����Ӱ�첻�󣡣����������ò��Ķ����е�����github��Ŀ�ϸ��Ҹ�`star`�ɡ����Ŀ϶�������˵�����Ķ�������