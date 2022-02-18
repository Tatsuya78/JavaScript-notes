# JavaScript-notes

#ES6

面向对象

面向对象更贴近我们的实际生活，可以使用面向对象描述现实世界事物。但是事物分为具体的事物和抽象的事物 

面向对象的思维特点


- 抽取（抽象）对象共用的属性和行为组织（封装）成一个类（模版）
- 对类进行实例化，获取类的对象

面向对象编程我们考虑的是有哪些对象，按照面向对象的思维特点，不断地创建对象，使用对象，指挥对象做事情


1. 对象

	现实生活中，万物皆对象，对象是一个具体的事物，看得见摸得着的实物。例如一本书、一辆汽车、一个人，都可以是对象，一个数据库、一张网页、一个与远程服务器的接连也可以是对象

	在JavaScript中，对象是一组无序的相关属性和方法的集合。所有的事物都是对象，例如字符串、数值、数组、函数等

	对象是由属性和方法组成的：


	- 属性：事物的特征，在对象中用属性来表示（常用名词）
	- 方法：事物的行为，在对象中用方法来表示（常用动词）
2. 类class

	在ES6中新增加了类的概念，可以使用class关键字声明一个类，之后以这个类来实例化对象

	类抽象了对象的公共部分，它泛指某一大类（class）

	对象特指某一个，通过类实例化一个具体的对象

	相当于图纸，模版。按这个图纸创建不同的对象

	而对象就只是这个对象，里面装有的是这个特指对象的属性和方法


3. 创建类

    ```javascript
    class Name {
    	// class body
    }
    
    var xx = new Name();
    ```

4. 类constructor构造函数

	constructor()方法是类的构造函数（默认方法），用于传递参数，返回实例对象，通过new命令生成对象实例时，自动调用该方法。如果没有显示定义，类内部会自动给我们创建一个constructor() 

    ```javascript
    class Star {
    	constructor(uname){
    		this.uname = uname;
    	}
    }
    var me = new Star（'Tatsuya');// new创建一个对象后会自动执行class模版里面的构造函数，传参
    console.log(me.uname); // Tatsuya
    ```


	由于其中的构造函数是因为new创建实例对象时触发执行的，所以类里面的this指向的是实例对象

	注意：


	1. 通过class关键字创建类，类名还是习惯性定义首字母大写
	2. 类里面有个constructor函数，可以接收传递过来的参数，同时返回给实例对象
	3. constructor函数只要new生成实例对象时就会自动调用，如果我们不写这个函数，类也会自动生成这个函数
	4. 生成实例对象new不能省略
	5. 最后注意语法规范，创建类，类名后面不要加小括号，生成实例，类名后面加小括号，构造函数不需要加function
	6. 多个函数方法之间不需要加逗号分隔
5. 类的继承
	- [ ] 继承

	显示中的继承：子承父业，比如我们继承了父亲的姓氏

	程序中的继承：子类可以继承父类的一些属性和方法

    ```javascript
    var Father {
    	constructor(){
    	
    	} // 不写构造函数也ok，创建类的时候系统会默认写一个
    	money(){
    		console.log('100');
    	}
    }
    
    var Son extends Father {
    
    }
    var son = new Son();
    son.money(); // 100
    ```

	- [ ] super关键字

    ```javascript
    class Father {
    	consturctor(x, y) {
    		this.x = x;
    		this.y = y;
    	}
    	// 可以直接把实例对象传递的参数都给构造函数
    	// 在构造函数中赋值给this.xx，这样this.xx相当于可以在这个类中使用的局部变量
    	// 这样就不用在类中的其他方法中再传递参数了
    	sum(){
    		console.log(this.x + this.y);
    	}
    }
    
    class Son extends Father {
    	constructor(x, y) {
    		this.x = x;
    		this.y = y;
    	}
    }
    
    var son = new Son(1, 2);
    son.sum(); // 这时会报错
    
    // Son确实继承了Father里的方法，但是Father里面的sum（）方法中
    // 的this.x和this.y指向的是Father中构造函数里的this.x和this.y
    // 换句话说就是继承的sum方法中的this.x和this.y是Father类中的局部变量
    // 1和2是复制给了Son中的局部变量this.x和this.y
    // Father类中的this.x和this.y是没有得到这两个数值的
    ```


	这样，如果能有什么方法把Son中的this.x和this.y传递给Father类，就能顺利的使用继承过来的sum方法了

	这就是super关键字的用处

	super关键字用于访问和调用对象父类上的函数。可以调用父类的构造函数，也可以调用父类的普通函数

	 

    ```javascript
    class Son extends Father {
    	constructor(x, y) {
    		// super(); 写了这句代码，就调用了父类中的构造函数
    		// 把参数传过去
    		super(x, y);
    	}
    }
    
    var son = new Son(1, 2);
    son.sum(); // 3
    ```


	super也能调用父类中的普通函数

    ```javascript
    class Father {
    	say(){
    		return '我是爸爸';
    	}
    }
    class Son extends Father {
    	say(){
    		console.log(super.say() + '的儿子');
    	}
    }
    var son = new Son();
    son.say(); // 我是爸爸的儿子
    ```


	注意：子类在构造函数中使用super，必须放到this前面（必须先调用父类的构造方法，再使用子类的构造方法）（先有了爸爸才能有孩子）


6. 三个注意点
	- 在ES6中类没有变量提升，所以必须先定义类，才能通过类实例化对象
	- 类里面共用的属性和方法一定要加this
	- 类里面this的指向问题

	constructor里面的this指向实例对象，方法里面的this指向这个方法的调用者


	- [ ] 案例：面向对象版tab栏切换

	功能需求：


	- 点击tab栏 可以切换效果
	- 点击+号，可以添加tab项和内容项
	- 点击x号，可以删除当前的tab项和内容项
	- 双击tab项文字或者内容项文字，可以修改里面的文字内容

	面向对象思路：

	抽象对象：tab对象。建立一个模版


	- 该对象具有切换功能
	- 该对象具有添加功能

	 

	以前的做法：动态创建元素craetElement，但是li里面内容较多，还需要innerHTML赋值，然后再appendChild

	高级做法：利用insertAdjacentHTML()可以直接把字符串格式元素添加到父元素中

	 

    ```javascript
    element.insetAdjacentHTML(position, text);
    
    // position是相对于element的位置
    // beforebegin 元素自身的前面
    // afterbegin 插入元素内部的第一个子节点之前
    // beforeend 插入元素内部的最后一个子节点之后
    // afterend 元素自身的后面
    ```


	 

	appendChild不支持追加字符串的子元素，insertAdjacentHTML支持追加字符串的元素


	- 该对象具有删除功能

	删除元素可用element.remove();


	- 该对象具有修改功能

	双击事件：ondblclick

	如果双击文字，会默认选定文字，此时需要双击禁止选中文字，代码如下：

	 

    ```javascript
    window.getSelection ? window.getSelection().removeAllRanges() : document.selection.empty();
    ```


	核心思路：双击文字的时候，在里面生成一个文本框，当失去焦点或者按下回车然后把文本框输入的值给原先的元素即可

	！！！重要代码，反复琢磨！！！

    ```html
    <body>
        <div class="tabsbox" id="tab">
            <div class="firstnav">
                <ul class="ul">
                    <li class="liactive">
                        <span>1</span>
                        <span class="icon-close">x</span>
                    </li>
                    <li>
                        <span>2</span>
                        <span class="icon-close">x</span>
                    </li>
                    <li>
                        <span>3</span>
                        <span class="icon-close">x</span>
                    </li>
                    <li>
                        <span>4</span>
                        <span class="icon-close">x</span>
                    </li>
                </ul>
                <div class="tabadd">+</div>
            </div>
            <div class="tabscon">
                <section class="conactive">1</section>
                <section>2</section>
                <section>3</section>
                <section>4</section>
            </div>
        </div>
        <script>
            var that;
            class Tab {
                constructor(id) {
                    // 获取元素 （通过id）
                    // 1. new的对象传递过来，右边获取过来的元素赋值给这个对象的主体盒子 所以this.main
                    that = this;
                    this.main = document.querySelector(id);
                    this.lis = this.main.querySelectorAll('li');
                    this.tabadd = this.main.querySelector('.tabadd');
                    this.ul = this.main.querySelector('ul');
                    this.tabscon = this.main.querySelectorAll('section');
                    this.tabsconBox = this.main.querySelector('.tabscon');
                    this.close = this.main.querySelectorAll('.icon-close');
                    // 只要new创建一个新tab栏，就先初始化一下，所以把init写到构造函数中
                    // new的那个实例对象执行init 所以this别忘写
                    this.init();
                }
                // 由于下面的功能都需要给每个li绑定onclick事件，所以需要先初始化
                init() {
                    this.updateNode();
                    for (var i = 0; i < this.lis.length; i++) {
                        this.lis[i].setAttribute('index', i);
                        // this.lis[i].onclick = this.toggleTab;
                        this.lis[i].addEventListener('click', that.toggleTab)
                        this.close[i].onclick = this.removeTab;
                        this.spans[i].ondblclick = this.editTab;
                        this.tabscon[i].ondblclick = this.editTab;
                    }
                    this.tabadd.addEventListener('click', that.addTab);
                }
                // 重新获取li和section
                updateNode(){
                    this.lis = this.main.querySelectorAll('li');
                    this.tabscon = this.main.querySelectorAll('section');
                    this.close = this.main.querySelectorAll('.icon-close');
                    // 由于span非常的多，且点击add键还会有新的span需要做特效，所以写在这里就好
                    this.spans = this.main.querySelectorAll('ul li span:first-child');
                }
                // 1. 切换功能
                toggleTab() {
                    // 排他思想，去掉其他人，留下我自己
                    that.removeClass();
                    this.className = 'liactive'
                    // 点击li，tabscon切换到相应的section
                    var index = this.getAttribute('index');
                    that.tabscon[index].className = 'conactive';
                }
                removeClass() {
                    for (var i = 0; i < that.lis.length; i++) {
                        that.lis[i].className = '';
                        that.tabscon[i].classList.remove('conactive');
                    }
                }
                // 2. 添加功能
                addTab() {
                    // 其余兄弟去掉active类
                    that.removeClass();
                    // a. 创建新的li和section
                    // 以前的做法：动态创建元素craetElement，但是li里面内容较多，还需要innerHTML赋值，然后再appendChild
                    // 高级做法：利用insertAdjacentHTML()可以直接把字符串格式元素添加到父元素中
                    var random = Math.random();
                    var li = '<li class="liactive"><span> new</span><span class="icon-close">x</span></li > '
                    var sec = '<section class="conactive">'+random+'</section>';
                    // b. 把创建的两个元素追加到对应的父元素中
                    that.ul.insertAdjacentHTML('beforeend', li);
                    that.tabsconBox.insertAdjacentHTML('beforeend', sec);
                    // 此时会出现bug，addTab里新增加的li和section无法用removeClass清楚类
                    // 因为removeClass里的this.lis可以看作一个变量，这个变量是一开始new了一个tab对象后就获取过来的原先存在的
                    // 解决：当点击了add按钮后 重新获取lis和sections然后绑定到clearClass中
                    // 即重新初始化init
                    that.init();
                }
                // 3. 删除功能
                removeTab(e) { 
                    // 阻止冒泡，点击关闭按钮会冒泡，li盒子也有点击事件也会触发
                    e.stopPropagation();
                    var index = this.parentNode.getAttribute('index');
                    that.ul.removeChild(that.lis[index]);
                    that.lis[index].remove();
                    that.tabscon[index].remove();
                    that.init();
                    // 当删除的不是选中状态的li，原来的选中状态li保持不变(即不要让index--)
                    if (document.querySelector('.liactive')) return;
                    index--;
                    // 手动调用点击事件，不需要鼠标触发,对比init中的不加(),且有切换section
                    // 短路运算，前面为真才执行后面代码
                    // 因为index--到-1 没有这个li 就会报错，所以先判断有没有这个li
                    that.lis[index] && that.lis[index].click();
                }
                // 4. 修改功能
                editTab() {
                    var str = this.innerHTML;
                    // 禁止双击选中文字
                    window.getSelection ? window.getSelection().removeAllRanges() : document.selection.empty();
                    // 双击span后，在这个span中添加一个input
                    this.innerHTML = '<input type="text" />';
                    var input = this.children[0];
                    this.children[0].value = str;
                    input.select(); // 让文本框里的内容变成选定状态
                    // 当离开文本框就把文本框里面的值给span
                    input.onblur = function(){
                        // 直接赋值给span了所以input也消失了
                        this.parentNode.innerHTML = this.value
                    }
                    //按下回车也可以把文本框的内容给span
                    input.onkeyup = function(e){
                        // 单个if可以用短路运算
                        e.keyCode === 13 && this.blur(); // 重要操作：手动调用事件
                    }
    
                }
            }
            // 可以根据这个Tab类创建不同的实例对象，我们页面中可能有很多Tab都需要从这个类（模版）
            // 中new出来（用来里面的功能），所以在new的时候需要区别一下
            // 现在要做的是id为tab的这一个tab栏
            new Tab('#tab');
    
        </script>
    </body>
    ```

