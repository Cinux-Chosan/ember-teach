`Ember`����`handlebars`ģ�����ΪӦ�õ�`view`�㡣`Handlebars`ģ������ͨ��`HTML`�ǳ����ơ����������ͨ��`HTML`����`handlebars`�ṩ�˷ǳ��ḻ�ı��ʽ��
`Ember`����`handlebars`ģ�岢����չ�˺ܶ๦�ܣ�����ʹ��`handlebars`����ʹ��`HTML`һ���򵥡�

### ģ�嶨��

��ǰһƪ������һ������Ҫ�Ĺ�������`Ember CLI`���ӱ�ƪ��ʼ�������������ļ�����ʹ����������������������Ƚ��뵽��Ŀ·������ִ��`Ember CLI`���

����һ��ģ������`ember g template application`

�������ģ���ڴ�����Ŀ��ʱ����Ѿ����ˣ����Ի���ʾ���Ƿ񸲸�ԭ�����ļ��������ѡ�񸲸ǻ��߲����Ƕ��С�

```html
<!-- app/templates/application.hbs -->
<h1>Kittens</h1>
<p>
Kittens are the cutest!!
</p>
```

**ע��**��<font color='red'>�����еĵ�һ��ע�͵����ݱ���������ļ���λ���Ѿ��ļ����ƣ�����Ĵ���Ƭ��Ҳ��������ַ�ʽ��ע�����û���ر��˵����һ����붼��ע���ļ���·���������ơ�</font>

��������һ��ģ�壬�ǳ��򵥵�ģ�壬ֻ��һ��h1��p��ǩ�����㱣������ļ���ʱ��Ember CLI���Զ�����ˢ��ҳ�棬����Ҫ���ֶ�ȥˢ�£���ʱ��������ҳ��Ӧ�ûῴ��������Ϣ��

![run result](/content/images/2016/03/15.png)

��ô��ϲ�㣬ģ�嶨��ɹ��ˣ�����Ϊʲôִ��[http://localhost:4200](http://localhost:4200)��ֱ����ʾ�������������ѧ��`controller`��`route`��ʱ����Ȼ�����ף���͵�`application.hbs`��һ��Ĭ�ϵ���ҳ��������Ӧ�������˰ɣ�

### handlbars���ʽ

ÿһ��ģ�嶼����һ����֮������`controller`�ࡢ`route`�ࡢ`model`�ࣨ��Ȼ��Щ���ǲ��Ǳ����еģ��������ģ������ʾ���ʽ��ֵ��ԭ���������`controller`��������ģ���б��ʽ��ʾ��ֵ������`java web`��������`servlet`����`Action`����`request.setAttribute()`��������ĳ������һ�������������ģ����룺

```html
<!-- app/templates/application.hbs -->

<!-- �����Ĭ�ϵ�ģ�壬Ember����������Ĺ����Զ��ҵ� controllers/application ��Ӧ��ģ����templates/application.hbs -->

<h2 id="title">Welcome to Ember</h2>

<!-- Ember�������Զ����£����������controller��ı��ˣ�ҳ����Զ�ˢ����ʾ���µ�ֵ��̫ǿ���ˣ����� -->

Hello, <strong>{{firstName}} {{lastName}}</strong>!
<br>
My email is <b>{{email}}</b>
```

�������Ǵ���һ��controller�����������Ember CLI��������� ember generate controller application����������ʾ�ᴴ��һ��controller����������application��Ȼ�����ǻ�õ����¼����ļ���

1. `app/controllers/application.js`   --`controller`����
2. `tests/unit/controllers/application-test.js`   --`controller`��Ӧ�ĵ�Ԫ�����ļ�

������ļ�Ŀ¼���ǲ��ǿ�����`app/controllers`���濴���ˣ�
����Ϊ����ʾ���ʽ������`controller`�����һЩ���룺

```java
// app/controllers/application.js

import Ember from 'ember';

/**
 * Ember��������������Զ��ҵ�templates/application.hbs���ģ�壬
 * @type {hash} ��Ҫ���õ�hash����
 */
export default Ember.Controller.extend({
	//  ������������
	firstName: 'chen',
	lastName: 'ubuntuvim',
	email: 'chendequanroob@gmail.com'
});
```

Ȼ���޸���ʾ��ģ�����£�

```html
<!-- app/templates/application.hbs -->

<!-- �����Ĭ�ϵ�ģ�壬Ember����������Ĺ����Զ��ҵ� controllers/application ��Ӧ��ģ����templates/application.hbs -->
<h2 id="title">Welcome to Ember</h2>

<!-- Ember�������Զ����£����������controller��ı��ˣ�ҳ����Զ�ˢ����ʾ���µ�ֵ��̫ǿ���ˣ����� -->
Hello, <strong>{{firstName}} {{lastName}}</strong>!
<br>
My email is <b>{{email}}</b>
```

���棬Ȼ��ҳ����Զ�ˢ�£�`Ember CLI`���Զ�����ļ��Ƿ�ı䣬Ȼ�����±�����Ŀ�������ǿ��Կ�����`controller`���õ�ֵ������ֱ����ģ������ʾ�ˡ�

![run result](/content/images/2016/03/16.png)

������Ǳ��ʽ�İ󶨣��������ѧϰ���������ȤҲ�����ӵ�`handlebasr`���ʽ��
����Ӧ�ó���Ĺ�ģ�������󣬻��и����ģ�����֮�����Ŀ�������������ʱ��һ��ģ�廹���Զ�Ӧ������������Ҳ����˵ģ���ϱ��ʽ��ֵ�����ж��`controller`���ơ�
<br>
���������������[Github](https://github.com/ubuntuvim/my_emberjs_code)�����ľ�������޸ģ������ϵĴ�����github��������ֳ��룬����Ӱ�첻�󣡣����������ò��Ķ����е��ã�����github��Ŀ�ϸ��ҵ��`star`�ɡ����Ŀ϶�������˵�����Ķ�������

