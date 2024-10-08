---
timezone: America/Los_Angeles
---


# Ye

1. 自我介绍
     - 清华-南加大 Communication Data Science 25'硕士在读，链上数据分析2年经验，Dune [@wyeeeh](https://dune.com/wyeeeh)。因为对链上数据的分析离不开合约解析，希望通过共学计划掌握Solidity的基础开发知识，能更好读懂合约的function和event。

2. 你认为你会完成本次残酷学习吗？
   - 有激励就有野心，之前完成过Sixdegree Lab和BuidlerDAO发起的Dune Analytics共学计划。
   
## Notes

<!-- Content_START -->

### 2024.09.23

#### WTF Academy Solidity 101.1 Hello Web3 (三行代码)
- IDE：[Remix IDE](https://remix.ethereum.org)
##### 合约
- 合约是 Solidity 中的一种结构，用于定义智能合约的代码和数据。
- 许可：如果不写许可，编译时会出现警告（warning），但程序仍可运行。
- 注释：单行注释 `//` ，多行注释 `/* */`
- 状态变量：状态变量是合约中声明的变量，用于存储合约的状态。
- 函数：函数是合约中用于执行特定任务的代码块。
- 函数修饰器：函数修饰器用于修改函数的行为。
- 事件：事件是合约中用于记录某些特定事件的代码块。
- 错误：错误是合约中用于记录某些特定错误信息的代码块。
- 部署：`Ctrl + S` 
  - 默认情况下，Remix 会使用 Remix 虚拟机（以前称为 JavaScript 虚拟机）来模拟以太坊链，运行智能合约，类似在浏览器里运行一条测试链。Remix 还会为你分配一些测试账户，每个账户里有 100 ETH（测试代币）
```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0; // 指定编译器版本

// 创建合约（contract），并声明合约名为 HelloWeb3，状态变量为 _string
contract HelloWeb3 {
    string public _string = "Hello Web3!"; 
}
```
- 变量名下划线
  - 私有变量：通常在变量名前加下划线，以表明这些变量是私有的。
  - 函数参数：有时在函数参数名前加下划线，以避免与状态变量名称冲突。
  - 状态变量：有时在状态变量名前加下划线，以便与局部变量区分开来。
  - 在例子中，_string 是一个状态变量，加下划线可能是为了与其他变量区分开来。
##### 测验结果
  - 75/100
  - 100/100

### 2024.09.24
#### WTF Academy Solidity 101.2 值类型

##### 值类型：Value Type，用于存储具体的值。
- 布尔类型：`true` 和 `false`。
- 整数类型：整数类型包括有符号整数（int）和无符号整数（uint）。

- 地址类型：地址类型用于存储以太坊地址。
  - 普通地址（address）: 存储一个 20 字节的值（以太坊地址的大小）。
  - payable address: 比普通地址多了 transfer 和 send 两个成员方法，用于接收转账。
- 字节数组
  - 定长字节数组: 属于值类型，数组长度在声明之后不能改变。根据字节数组的长度分为 bytes1, bytes8, bytes32 等类型。定长字节数组最多存储 32 bytes 数据，即bytes32。
  - 不定长字节数组: 属于引用类型（之后的章节介绍），数组长度在声明之后可以改变，包括 bytes 等。
- 枚举 enum
  - 枚举（enum）是 Solidity 中用户定义的数据类型。它主要用于为 uint 分配名称，使程序易于阅读和维护。

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.4;

contract ValueTypes {
    // 布尔值
    bool public _bool = true; 

    // 布尔运算
    bool public _bool1 = !_bool; // 取非
    bool public _bool2 = _bool && _bool1; // 与
    bool public _bool3 = _bool || _bool1; // 或
    bool public _bool4 = _bool == _bool1; // 相等
    bool public _bool5 = _bool != _bool1; // 不相等

    // 整型
    int public _int = -1; // 整数，包括负数
    uint public _uint = 1; // 正整数
    uint256 public _number = 20220330; // 256位正整数

    // 整数运算
    uint256 public _number1 = _number + 1; 
    uint256 public _number2 = 2**2; // 指数
    uint256 public _number3 = 7 % 2; // 取余数
    bool public _numberbool = _number2 > _number3; // 比大小

    // 地址
    address public _address = 0x7A58c0Be72BE218B41C608b7Fe7C5bB630736C71;
    address payable public _address1 = payable(_address); // payable address，可以转账、查余额
    // 地址类型的成员
    uint256 public balance = _address1.balance; // balance of address

    // 固定长度的字节数组
    bytes32 public _byte32 = "MiniSolidity"; 
    
    // bytes32 是一个固定长度的字节数组，长度为 32 字节。"MiniSolidity" 是一个字符串字面量，它会被自动转换为字节数组并存储在 _byte32 中。由于 bytes32 的长度是 32 字节，而 "MiniSolidity" 的长度小于 32 字节，剩余的字节会被填充为零。

    bytes1 public _byte = _byte32[0]; 
    // _byte 是 _byte32 的第一个字节，因此 _byte 的值为 "M"。

    // 枚举 enum
    // 用enum将uint 0， 1， 2表示为Buy, Hold, Sell
    enum ActionSet { Buy, Hold, Sell }
    // 创建enum变量 action
    ActionSet action = ActionSet.Buy; // 实际上在内存中存储的是整数0

    // enum可以和uint显式的转换，返回当前action的整数值
    function enumToUint() external view returns(uint){
        return uint(action);
    }

}

//deploy后可以在VALUETYPES找到声明的变量。
```

##### 测验错题
  1. solidity中数值类型(Value Type)不包括float
  2. 下列代码的意思是
   
      ```solidity
      address payable addr;
      addr.transfer(1);
      ```
     - `address payable addr;`：声明了一个可支付的以太坊地址变量 `addr`。`payable` 关键字表示这个地址可以接收以太币（Ether）。
     - `addr.transfer(1);`：将 1 wei（以太坊的最小单位）转账到 `addr` 地址。`transfer` 方法用于从合约中转移以太币到指定的 `payable` 地址。
     - 这段代码定义了一个可以接收以太币的地址，并向该地址转账 1 wei。
  3. bytes4类型具有8个16进制位

### 2024.09.25
#### WTF Academy Solidity 101.3 函数

##### Solidity中函数的形式

  ```Solidity
  function <function name>(<parameter types>) {internal|external|public|private} [pure|view|payable] [returns (<return types>)]
  ```
 ##### function：声明函数
  - `<function name>`：函数名。
  - `(<parameter types>)`：参数，输入到函数的变量类型和名称
  - `{internal|external|public|private}`：函数可见性说明符，共有4种。
    - public：内部和外部均可见。
    - private：只能从本合约内部访问，继承的合约也不能使用。
    - external：只能从合约外部访问（但内部可以通过 this.f() 来调用，f是函数名）。
    - internal: 只能从合约内部访问，继承的合约可以用。
    - 注意 1：合约中定义的函数需要明确指定可见性，它们没有默认值。
    - 注意 2：public|private|internal 也可用于修饰状态变量。public变量会自动生成同名的getter函数，用于查询数值。未标明可见性类型的状态变量，默认为internal。
  - `[pure|view|payable]`：决定函数权限/功能的关键字。payable（可支付的）很好理解，带着它的函数，运行的时候可以给合约转入 ETH。pure 和 view 的介绍见下一节。
  - `[returns ()]`：函数返回的变量类型和名称。
##### Pure和View
  - 包含 pure 和 view 关键字的函数是不改写链上状态的，因此用户直接调用它们是不需要付 gas 的。
    - pure 函数既不能读取也不能写入链上的状态变量。
    - view函数能读取但也不能写入状态变量。
  - 非 pure 或 view 的函数既可以读取也可以写入状态变量。合约中非 pure/view 函数调用 pure/view 函数时需要付gas。
##### internal v.s. external
  - `internal` 函数只能由合约内部调用
  - 我们必须再定义一个 `external` 的 `minusCall()` 函数，通过它间接调用内部的 `minus()` 函数。
##### payable
  - 运行的时候可以给合约转入 ETH。
##### 测验结果
  - 100/100

### 2024.09.26
#### WTF Academy Solidity 101.4 函数输出

##### 返回值：return 和 returns
- return 和 returns 都可以用于返回值，但它们的使用场景不同。
  - `returns`：跟在函数名后面，用于声明返回的变量类型及变量名。
  - `return`：用于函数主体中，返回指定的变量。

```solidity
// 返回多个变量
function returnMultiple() public pure returns(uint256, bool, uint256[3] memory){
    return(1, true, [uint256(1),2,5]);
}
```
- returns(uint256, bool, uint256[3] memory) 表示该函数将返回3个值：
  - 第一个是 uint256 类型。
  - 第二个是 bool 类型。
  - 第三个是长度为3的 uint256 数组。
- return (1, true, [uint256(1), 2, 5]) 实际返回的值是：
  - 1 作为第一个返回值，类型为 uint256。
  - true 作为第二个返回值，类型为 bool。
  - [1, 2, 5] 作为第三个返回值，类型为 uint256[3]。
- memory 修饰符用来声明数据的存储位置。
  - 在Solidity中，数组作为返回值时，通常需要指定存储位置。可以是 memory（临时存储）或 storage（持久存储在区块链上）。函数返回的数组通常存储在内存中，因此我们使用 memory 修饰符。
- 类型转换
  - 在Solidity中，类型转换通常用于将一个数据类型转换为另一个数据类型。
  - 假设有一个数组，要求所有元素都必须是 uint256 类型，如：
    ```solidity
    uint256[3] memory myArray;
    ```

    但输入了以下内容：

    ```solidity
    myArray = [1, 2, 5];
    ```

    编译器会认为 1, 2, 5 都是最小的适合类型（可能是 uint8）。然而，数组的类型被声明为 uint256，因此编译器会提示类型不匹配。为了避免这种错误，你需要显示地告诉编译器，第一个元素 1 是 uint256 类型：

    ```solidity
    myArray = [uint256(1), 2, 5];
    ```

    这样，编译器就知道，所有元素的类型都是 uint256，符合数组的要求。

##### 命名式返回
- 用 `returns(uint256 _number, bool _bool, uint256[3] memory _array)` 声明了返回变量类型以及变量名。这样，在主体中只需为变量 `_number`、`_bool`和`_array` 赋值，即可自动返回。

```solidity
// 命名式返回
function returnNamed() public pure returns(uint256 _number, bool _bool, uint256[3] memory _array){
    _number = 2;
    _bool = false;
    _array = [uint256(3),2,1];
}

// 命名式返回，依然支持return
function returnNamed2() public pure returns(uint256 _number, bool _bool, uint256[3] memory _array){
    return(1, true, [uint256(1),2,5]);
}
```

##### 解构式赋值
- 读取所有返回值：声明变量，然后将要赋值的变量用`,`隔开，按顺序排列。
- 读取部分返回值：声明要读取的返回值对应的变量，不读取的留空。我们只读取`_bool`，而不读取返回的`_number`和`_array`

```solidity
uint256 _number;
bool _bool;
uint256[3] memory _array;

// 读取所有返回值
(_number, _bool, _array) = returnNamed();

// 读取部分返回值
(, _bool2, ) = returnNamed();
```

##### 测验结果
- 100/100


### 2024.09.27
#### WTF Academy Solidity 101.5 变量数据存储和作用域 storage/memory/calldata

##### 引用类型(Reference Type)
- 包括数组（array）和结构体（struct），由于这类变量比较复杂，占用存储空间大，我们在使用时必须要**声明数据存储的位置**。

##### 数据位置
- 不同存储位置的`gas`成本不同。
  - `storage`类型的数据存在链上，类似计算机的硬盘，消耗`gas`多；
  - `memory`和`calldata`类型的临时存在内存里，消耗`gas`少。
1. `storage`：合约里的状态变量默认都是`storage`，存储在链上。

1. `memory`：函数里的参数和临时变量一般用`memory`，存储在内存中，不上链。尤其是如果返回数据类型是变长的情况下，**必须加memory修饰**，例如：string, bytes, array和自定义结构。

2. `calldata`：和`memory`类似，存储在内存中，不上链。与`memory`的不同点在于`calldata`变量不能修改（`immutable`），一般用于函数的参数。

##### 赋值规则
| 赋值类型 | 是否为引用 | 备注 |
| --- | --- | --- |
| **Storage** ↔ **Storage** | 引用 | 除非赋值给状态变量或存储结构体成员，创建副本 |
| **Memory** ↔ **Memory** | 引用 | Memory 变量共享同一数据，修改会互相影响 |
| **Storage** → **Memory** | 独立副本 | 从 `storage` 到 `memory` 创建副本，修改 memory 变量不会影响 `storage` 数据。 |
| **Memory** → **Storage** | 独立副本 | 从 `memory` 到 `storage` 创建副本 |
| **Calldata** → **Memory** | 独立副本 | `calldata` 到 `memory` 创建副本 |
| **Calldata** → **Storage** | 独立副本 | `calldata` 到 `storage` 创建副本 |

##### 变量的作用域
1. 状态变量（state variable）
     - 状态变量是数据存储在链上的变量，所有合约内函数都可以访问，gas消耗高。
2. 局部变量（local variable）
     - 局部变量是仅在函数执行过程中有效的变量，函数退出后，变量无效。局部变量的数据存储在内存里，不上链，gas低。
3. 全局变量（global variable）
     - 全局变量是全局范围工作的变量，都是solidity预留关键字。他们可以在函数内不声明直接使用
     - 时间单位

##### 测验结果
- 100/100

### 2024.09.28
#### WTF Academy Solidity 101.6 引用类型, array, struct

##### 数组 Array
- 存储在 `storage` 的数组：
    - **可变长度数组**（即未指定固定长度的 `T[]`）是可以动态扩展和缩减的，例如通过 `push()` 和 `pop()` 操作。
    - **固定长度数组**（如 `uint[8]`）在 `storage` 中长度是固定的，初始化后不能改变其长度。
- 存储在 `memory` 的数组：
    - **可变长度数组**在 `memory` 中一旦初始化，**长度是固定的**，不能在运行时再改变长度。因此，`memory` 数组在初始化时必须指定其长度，之后无法扩展或缩减。

**数组成员**
- `length`: 可以读取数组的长度。`memory`数组的长度在创建后是固定的，`storage` 数组可以通过直接赋值来修改数组长度。
- `push()`: 向 `storage` 中的可变长度数组添加一个`0`元素，并返回该元素的引用。
- `push(x)`: 向 `storage` 中的可变长度数组添加一个`x`元素，并自动增加数组的长度。
- `pop()`: 删除 `storage` 数组的最后一个元素，并减少数组的长度。

- 注意事项
  - `storage` 数组：支持 `.push()`、`.pop()` 和 `.length` 成员，可以动态增加和减少长度。
  - `memory` 数组的操作相对简单，因为它们的长度一旦初始化后无法改变。因此，只有读取和修改数组元素的功能，没有 `push` 和 `pop` 操作。
  - 对于固定长度的数组（无论在 `storage` 还是 `memory`），它们的长度在编译时就确定了，因此无法使用 `.push()` 或 `.pop()` 操作。

```Solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract StorageArrayLength {
    uint[] public array;

    // 获取数组长度
    function getLength() public view returns (uint) {
        return array.length;
    }

    // 修改数组长度
    function setLength(uint newLength) public {
        array.length = newLength;
    }
}

contract StorageArrayPush {
    uint[] public array;

    // 向数组中添加元素
    function addElement(uint _value) public {
        array.push(_value);
    }

    uint[] public numbers;

    function addElement() public {
        uint storageElement = numbers.push(); // 添加一个0元素并返回其引用
        numbers[numbers.length - 1] = 42;     // 可以通过引用直接修改最后一个元素
      }
}
```

##### 结构体 struct
`struct` 是 Solidity 中用于定义自定义类型的关键字。每个结构体可以包含不同类型的变量，称为字段（fields），它们可以是基本类型（如 `uint`、`bool` 等）或引用类型（如数组、映射等）。
1. **定义结构体**
     - 这是为了创建一种新的数据类型，类似于定义一个模版。定义结构体是告诉 Solidity，接下来可以使用这种新的自定义类型，类似于在其他编程语言中定义一个类（class）或数据类型。
    ```solidity
    // 定义一个名为 Student 的结构体
    struct Student {
        uint256 id;     // 学生ID
        uint256 score;  // 学生分数
    }
    ```

2. **声明结构体变量**
    - 这是在定义的结构体类型基础上创建一个实际的变量，并分配内存。声明结构体变量后，可以使用它来存储和操作数据。
      ```solidity
      Student student; // 声明一个 `Student` 结构体变量
      ```

3. **赋值方式**
    - `storage` 引用：在函数中创建一个指向状态变量的 `storage` 引用，可以直接修改该结构体。
      ```solidity
      function initStudent1() external {
          Student storage _student = student; // 指向 `student` 结构体的引用
          _student.id = 11;                   // 修改 `student` 的 id
          _student.score = 100;               // 修改 `student` 的 score
      }
      ```

      在这个例子中，`_student` 是对状态变量 `student` 的引用。通过修改 `_student`，你实际上是在修改原始 `student` 结构体。

    - 直接修改结构体字段：直接引用结构体变量并为其字段赋值。
      ```solidity
      function initStudent2() external {
          student.id = 1;        // 直接修改 `student` 的 id
          student.score = 80;     // 直接修改 `student` 的 score
      }
      ```
      在这种方法中，直接操作状态变量 `student`，而不需要创建中间的引用。
    - 构造函数式：利用构造函数风格的赋值方法为结构体赋值。
      ```solidity
      function initStudent3() external {
          student = Student(3, 90);  // 使用构造函数语法为 `student` 赋值
      }
      ```
      这种方法类似于函数调用，通过提供参数来一次性赋值结构体的所有字段。
    - `key-value` 形式赋值：这种方式允许通过 `key-value` 的形式为结构体赋值，特别适用于具有很多字段的结构体。
      ```solidity
      function initStudent4() external {
          student = Student({id: 4, score: 60});  // 通过键值对形式赋值
      }
      ```
      `key-value` 方式在参数顺序不重要或者字段较多时，能提高代码的可读性。

##### 测验结果
- 100/100


### 2024.09.29
#### WTF Academy Solidity 101.7 映射类型 mapping


<!-- Content_END -->
