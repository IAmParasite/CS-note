## 密码学笔记

> 18373059 胡鹏飞

### 第一章 引论

- 密码学发展三个阶段：古典密码（艺术）、近代密码、现代密码（1976年以后）
- 古典密码代表：凯撒密码（移位密码、单表密码 字母a用字母D代替...）、维吉尼亚密码（多表代换）
- 单表密码：相同的明文必然产生相同的密文
- 多表密码：将26个移位密表合成一个“维吉尼亚密表”
- 攻击
  - 对机密性的攻击：窃听、流量分析
  - 对完整性的攻击：篡改、伪装、重放、否认
  - 对可用性的攻击：拒绝服务
    被动攻击：内容泄露（窃听）、流量分析
    主动攻击：伪造（伪装）、中断（拒绝服务）、修改（改变、重放）
- 安全威胁：病毒、蠕虫、木马、小程序（控件）、Cookise、脚本
- 安全服务：加密保护机密性、保护完整性、身份认证、不可否认性、访问控制
- 安全机制：加密、信息完整性、数字签名、身份认证交换、流量填充、路由控制、公证、访问控制
- 安全技术：密码术、密写术
- 1883年Kerchoffs第一次明确提出了编码的规则：加密算法应建立在算法的公开不影响明文和密钥的安全（传统密码和现代密码的分界线）
- 公钥密码使得发送端和接收端无密钥传输的保密通信成为可能
- 1977年DES正式称为标准...
- 密码学、密码编码学、密码分析学
- P-明文，C-密文，变换记为$C=E(p)$及$P=D(C)$同时满足$P=D(E(P))$，需要密钥的加密算法$C=E(K,P)$，加密和解密的密钥相同$P=D(K,E(K,P))$，不同的为$P=D(K_D,E(K_E,P))$
- 密码体系是一个五元组(P,C,K,E,D) 
- 古希腊密码：5*5的密码表
- 密码分析（破译）是在不知道密钥的情况下，恢复出明文的科学
  - 试图破译单条消息
  - 试图识别加密的消息格式
  - 试图找到加密算法的普遍缺陷
- 密码泄露：通过非密码分析方式丢失
- 唯密文攻击、已知明文攻击、选择明文攻击、自适应选择明文攻击选择密文攻击、选择文本攻击、选择密钥攻击
- 攻击方法：蛮力攻击、穷举攻击、统计攻击、模式攻击、软磨硬泡攻击
- 无条件安全：无论提供的密文有多少，如果由一个加密方案产生的密文中包含的信息不足以唯一地决定对应地明文。除了一次一密地方案没有无条件安全的算法
- 密码安全性体现在：破译成本超过加密信息的价值、破译时间超过该信息有用的生命周期
- 攻击的复杂性分析：数据复杂性、处理复杂性、存储需求

### 第二章 密码数学

- $n|a$ n整除a，a是n的因子

- $gcd$最大公因子 greatest common divisor

- 定理：$gcd (a, 0) = 0$

- 定理：$gcd (a, b) = gcd (b, r)$ 其中 $a = q * b + r$

- 定理：$gcd (a, b) = d$，必存在证书s, t 使 d = s * a + t * b 如：gcd (726, 393) = 3 表示为 s * 726 + t * 393 其中 s = -59, t = 109

- 若$ gcd (a, b) = 1$, 必存在整数 s 和 t，使 $ s * a + t * b = 1 $

- 线性丢番图方程的解法：$ax+by=c$ 

  - 求出 $d = gcd (a,b)$
  - 若$d|c$，则方程两边同除以$d$，化为同解方程 $a_1 x+ b_1 y = c_1$, 此时$gcd(a_1, b_1) =1 $
  - 扩展欧氏算法求出 $s*a_1+t*b_1=1$
  - 同乘以 $c_1$，得到$(c_1*s)*a_1+(c_1*t)*b_1=c_1$
  - 特解：$x_0=c_1*s, y_0=c_1*t$
  - 得到通解$x=x_0+k*b_1; y = y_0-k*a_1$
  - **若$d$不能整除$c$，则无解**

- $(a\pm b)\mod n = (a \mod n)\pm(a \mod n)$
  $(a\times b)\mod n=(a \mod n)\times (a \mod n)$

- 模11, 5, 3, 9 有特殊方法

- 加法逆：$a+b=0\mod n$

- 乘法逆：$a\times b=1 \mod n, b=a^{-1}$

- a有乘法逆 $\Leftrightarrow$$gcd(a,n)=1$

- 加法集$Z_n$，乘法集${Z_n}^*$

- 若$gcd(|A|, n) 1$，则存在$A^{-1}\mod n$

- $A^{-1}$为矩阵中每一个元素$a_{ij} \mod n$

- 模n线性方程组 $ax=b \mod n$的解

  - 若$gcd(a,n)=d, 且d|b$，则方程有$d$个解
    两端除以$d$： $(a/d)x=(b/d)mod(n/d)$
    化为：$a_1 x = b_1 \mod n_1$

    由于：$gcd(a_1,n_1)=1$，$a_1$可$\mod n_1$
    特解：$x_0={a_1}^{-1}b_1$

    通解：$x=x_0+k*n_1, k = 0,1,2,\ldots, d-1$
    
  - 若$gcd (a,n)=1$，则方程有唯一解
  
  - 若$gcd(a,n)=d$，且$d$不整除$b$，则方程无解
  
- $a$为素数时有唯一解，$x=a^{-1}b\mod n$
  
- 线性方程组用矩阵的逆来求解

### 第三章传统密码学
- 代换密码

  - 单码代换：$Z_{26}\rightarrow Z_{26}$，一共有$26!$种一对一的映射
- 凯撒密码：$C=E(P)=P+3$...
  
  - 加法密码：$C=(P+k)\mod 26$...
- 乘法密码：$C=(P\times k)\mod 26$...，域大小较小$Z_{26}^*$的阶为$12$
  - 仿射密码：$C=(P\times k_1 + k_2)\mod 26$...
  - 单表密码：建立一张字母映射表一一映射 $26!$，常用的是在字母表中首先排泄出密钥字中出现的字母 不能抵抗频率统计攻击
- 多码代换：明文中的一个字符被代换成密文中的多个字符，明文与密文中的字符总是一对多的对应关系 $Z_{26}\rightarrow Z_{26}$的一对多的映射
  
  - 自动密钥密码：$C_i=P_i+K_i\mod 26$... 选一个字母作密钥，放到密钥流的最前面，然后接上明文$P$，密码域为$26$
  - PlayFair密码："同行右移、同列下移、否则对角、揭秘反向"，密码域$25! $  一战中使用
  - Vigenere密码：密钥$k=(k_1k_2k_3\ldots k_m),m\leq26$循环使用 $C_i=P_i+k_i\mod 26$ 实际为分组密码，怎组大小=密钥字的长度
  - Hill密码：密钥$K=(k_{ij})_{m\times m}$明文分成长度为$m$的分组，写成矩阵$P_{r\times m}$ $C = P * K \mod 26$...
  - 一次一密密码$OPT$ $C_i=P_i*K_i\mod 26$ ，加密下一条信息时，更换密码，使用非重复的随机字母序列加密，会使至今能使用的任何密码分析工具失效
  - 长随机数序列（对OPT的近似实现）: $r_{i+1}=r_i*c+b \mod w$
- 换位密码：字母本身不变，但位置变了
  - 无密钥换位：
    - 栅栏密码（分成两栏：偶数一排，奇数一排）
    - 表格换位：将明文字符分割成五个一行的分组，排进表格中
  - 有密钥换位：密钥K就是一个指定的置换，矩阵乘法也可以表示换位 
  - 双换位：将换位方法重复两次——讲过两次换位盒
  - 组合换位：不同密钥，多次组合
  - 换位密码的分析：
    - 频率攻击：特征：保留单字频率，但不保留双字母、三字母频率 攻击：判断是换位密码，然后单字母频率攻击
    - 蛮力攻击：
      - 遍历所有可能的20字母排列，$20!$
      - 遍历所有可能的$k$ 
      - 猜测列数
    - 模式攻击（猜测列数）：寻找字母位置的排布模式，进而猜测列数$n$
  - 密码机
    - 转轮密码（rotor cipher）
    - Enigma密码机：安全分析等...

### 第四章密码数学B

- 群(group)：非空集合$G$，$*$为定义在$G$上的二元运算，如果满足运算封闭性、结合律、存在单位元$a*e=e*a=a$、存在逆元$a*a^{-1}=a^{-1}*a=e$

- 交换群：满足交换律 $a*b=b*a$

- 置换群：

  <img src="11.png" alt="image-20210616142901335" style="zoom:50%;" />

- 有限群：元素个数有限 $|G|$表示
- 循环群：$G$的元素可以由一个元素$g$（生成元/本原根）及其幂组成
- $Lagernge$定理：子群$H$的阶数一定是$|G|$的因子，子群要满足群的定义
- 元素a的阶：满足$a^n=e$的最小整数 记为 $ord(a)$等于由$a$生成的循环子群的阶数 这里的幂为满足群的运算
- 环：加减乘
- 域：加减乘除
- $Galois$指出：有限域的元素个数必为$p^n$，因此有限域又称伽罗华域，记为$GF(p^n)$
- 素域$GF(p)$：四则运算就是 $ \mod p$运算，加与乘都具有消去律，非0元素都有逆元，非0元素都可以用生成元表示为$a=g^i, a^{-1}=g^{-i\mod (p-1)}$
- 欧拉定理：$\mod p$运算中，对任意非$0$的元素$a$总有$a^{p-1}=1 \mod p$，$p$为素数
- 伽罗华域$GF(2^n)$：
  - 做减法就是做加法
  - 模2加：异或
  - 模2乘：布尔
  - 模运算：保证乘法运算的封闭性，同时保证任何非0元素都有逆
  - 定理：$s(x)p(x)+t(x)q(x)=1$，其中$p(x),q(x)$互素
  - 定理：如果$p(x)$是$n$次不可约多项式，则任何低于$n$次的多项式$A(x)$，必存在唯一的$A^{-1}(x)$使得 $A(x)*A^{-1}(x)=1 \mod p(x)$
  - 求逆的方法：扩展的欧几里得算法、使用生成元方法
  - 利用生成元的四则运算：$x^p*x^q=x^{(p+q)\mod (2^n-1)}, (x^p)^{-1}=x^{(-p)\mod (2^n-1)}$
  - 乘除法是指数上的加减法 $\mod (2^n-1)$
  - 矩阵运算...

### 第五章现代对称密码体制

- 1977年DES由IBM设计并正式由NBS公布使用(National Bureau of Standards)
- DES: Data Encryption Standard 数据加密标准 满足8个条件
- AES： Advanced Encryption Standard 高级加密标准 2000年10月2日获胜者为 Rijndael 算法 2003年2月 Camellia作为NESSIE的128位分组密码标准
- 基本要求：分组足够长、密钥域足够大、密码变换足够复杂（扩散和混淆）、雪崩效应特性足够好
- 基本机密方法——代换（换字盒）和置乱盒（换位盒）
  - 全密钥换位密码 密钥域$n!$
  - 全密钥换字密码 密钥域$2^n!$
  - 部分密钥密码：部分可能的换位和换字
  - 无密钥换位密码：换位盒——P-box 直接换位盒、压缩换位盒、扩展换位盒
  - 无密钥代换密码：换字盒——S-box 是一个非线性、不可逆的映射，其作用是充分实现混淆功能
- 现代对称密码的常用运算
  - 按位异或运算
  - 移位、循环移位运算
  - 按位或、与、非运算
  - 交换运算
  - 分裂与整合运算
- Fistel结构（含有不可逆构建）PPT后三页

### 第六章 数据加密标准DES (Data Encryption Standard)

- DES加密算法是一个对称算：加密和解密用同一算法和密钥
- DES加密算法是分组密码：明文分成64位的分组进行加密，输出64位密文
  密文长度64位，其中56位密钥，8位校验位
- DES采用混乱和扩散两种最佳本的加密技术
- DES 16轮，每轮结构相同：每一轮采用Fistel结构
- 扩散：使得明文和密文之间的统计关系尽量复杂
- 混乱：使得密文的统计特性与密钥的取值之间的关系尽量复杂
- DES结构的结构：
- $C = DES(M)=IP^{-1}\circ T_{16} \circ T_{15}\ldots T_{1} \circ IP(M)$
- 初始置换和最终置换互逆，都是64-64位换位盒
- $f(R_{i-1},K_i) =PS(K_i\oplus E(R_{i-1}))$，P位直接换位盒，E为扩展换位盒，S为8个换字盒
- 加解密过程中最后一轮没有交换和
- $Li=R_{i-1},$ $R_i=L_{i-1}\oplus f(R_{i-1}, K_i)$
- DES的密钥生成器结构：
- 弱密钥K: 初始密钥K经PC-1置换后$C_0$和$D_0$全是0或全是1，则16个子密钥完全相同 一共有4个弱密钥
- 半弱密钥：存在一对密钥K和$K'$使得$DES_K(M)=DES_{K'}^{-1}(M)$ 一共有12个半弱密钥
- IDEA: 国际数据加密算法 明文为分组长度64位，密钥：解密密钥和加密密钥不同，长度均为128位
- 其他分组对称密码：Serpent密码，Twofish 密码 CAST-128,-256密码，$SAFFR^+$ MARS密码 TEA密码

### 第七章 高级加密标准AES

- 算法为 Rijndael 算法 输入输出为128位
- 总体结构为：10, 12, 14 128, 192, 256
- 128位分成16字节，排成一个$4\times 4$的矩阵
- AES轮的结构 换字盒 -> 行移位 -> 列混合 -> 轮加密
  - 换字盒SubBytes 是唯一非线性变换，起混乱作用，防止差分和先行密码分析方法的攻击
  - 行移位：扩散作用
  - 列混合：$GF(2^8)$ 扩散作用
  - 加轮密钥：循环密钥同上层结果进行异或运算
- 密钥扩展
- AES没有弱密钥
- 看ppt

### 第八章 Camellia

- Camellia 和 AES作为NESSIE的128位分组密码标准
- 128位分组密码：明文和密文同为128位 
- 主密钥（种子密钥）：128 192 256
- 18轮 Fistel
- 首先进行预白化处理，每6轮fistel迭代后嵌入$FL/FL^{-1}$变换层
- 压缩函数$F(L_{r-1},L_r)$64位

### 第九章 分组密码的连接

- 5种操作模式：ECB CBC CFB OFB CTR
- $ECB$ 电子密码本 把任意长文件分成64位或128位的分组 各个分组都用同一个密码K、用相同方法加密 计算效率高，运算快
- $CBC$ 密码分组连接: 每一分组与前组的密文作异或之后，再加密 第一个分组与初始向量(IV)作异或
  - 初始IV由收发双方共享，要像密钥一样保护
  - 单个错误可以自我恢复
  - 隐藏了明文的频率特性，对抗统计攻击
  - 不能并行
- 计数器$CTR$模式 每加密一次，计数器会增$1$
  - 同步流密钥，其密钥流由计数器产生
  - 守法双方计数器初始值必须保持一致
  - 分组层不保留
  - 避免了错误的传播
  - 分组大小与DES或AES相同
- 密码反馈$CFB$：移位寄存器$L_{i-1}$向左移动$j$位，用$j$位密文$C_{i-1}$反馈至移出的空位进行填充，构成新的寄存器$L_i$
  - 本质上是一种流密钥
  - 移位寄存器的长度位$L$，每次移出$j$位
  - 明文和密文的长度都是$j$位
  - 密钥流机制，不保留分组层
  - 差错传播的影响程度远大于$CBC$
- 输出反馈$OFB$
  - 反馈的不是前一个密文$C_i$，二十移位寄存器所移出的$j$位数据
  - 用于加密小的明文分组
  - 适合带噪信道上的数据传输（卫星通讯）

### 第十章 密码数学C

- $\pi(n)$小于等于$n$的素数的个数
- 埃拉托色尼筛法：100以内的所有素数，不能背2，3，5，7整除的数一定是素数
- $Mersenne(梅森)$素数：$M_p=2^p-1$
- $Fermat(费马)$素数：$F_n=2^{2n}+1$
- 素数测试：
  - 整除性检验：复杂度指数$O(2^{n_b/2})$
  - $Fermat$
  - 平方根检验
  - $Miller-Tabin$检验 -- 概率素性测试算法
  - AKS检验 $O(log_2n_b)^{12}$
- 因式分解
  - 试除法
  - $Fermat$方法
  - $Pollard p -1$ 方法
  - $Pollard \ \rho$
  - 二次筛法
  - 数字域筛法
- 任何大于1的正整数$n$都可以表示为素数幂的乘积
- 欧拉函数$\Phi(n)$位小于$n$且与$n$互素的非负整数的个数
- 定理：$\Phi(p)=p-1$
- 定理：若$m,n$互素，则$\Phi (m \times n) = \Phi (m)*\Phi(n)$
- 定理：若$p$是素数，则$\Phi(p^e)=p^e-p^{e-1}=p^e(1-\frac1p)$
- 推论：$\Phi(m)=m(1-\frac1{p_1})(1-\frac1{p_2})\ldots(1-\frac1{p_k})$
- 定理：若$p$是素数，$(a,p)=1$ 则$a^{p-1}=1\mod p$
- 定理：若$p$是素数，$a$是整数，则$a^p=a\mod p$
- 推论：若$p$是素数，$(a,p)=1$，则$a^{-1}=a^{p-2}\mod p$
- 定理：若$a,n$互素，则$a^{\varphi(n)}=1 \mod n$
- 定理：若$a \lt n, k$是整数，则$a^{k\phi(n)+1}=a \mod n$
- 推论：若$gcd(a,n)=1, a\lt p$，则$a^{-1}=a^{\phi(x)-1}\mod p$
- 中国剩余定理解线性同余方程组：
  - 套公式
- 二次同余： $x^2\equiv4 \mod 5$
- 引理：若$p$是奇素数，$p$与$a$互素，则$x^2\equiv a \mod p$ 或无解，或由两个模$p$不同余的解 $1\leq x' \lt p$是一解，则另一解位$p-x'$
- 解称为$QR$(平方同余)： 否则 $QNR(非平方同余)$
- 若$p$是寄素数，则$1,2,\ldots,p-1$中恰好有$(p-1)/2$哥数是$\mod p$平方同余；另外的数是非平方同余
- 定理：设$p$是奇素数 若 $a^{(p-1)/2}=1 \mod p$则$a$是平方同余；若$a^{(p-1)/2}=-1\mod p$则$a$是非平方同余
- 定理：设$p=4k+3$，$a$是平凡同余，则$x^2\equiv a \mod p$的解是 $x=a^{(p+1)/4}\mod p$ $x=-a^{(p+1)/4}\mod p$
- $\mod n $时二次同余式的求解：设$n=p_1p_2\ldots p_k$求解 $x^2\equiv a \mod p_1$   $x^2\equiv a \mod p_2$ $\ldots$  $x^2\equiv a \mod p_n$  
- 指数与离散对数...

### 第十一章公钥密码体制

- 公钥加密、私钥解密：$C=f(K_{public}, P)$ $P=g(K_{private},C)$
- 单向陷门函数（TOWF）加密容易，解密困难
  - 单向：$y=f(x) ,x=f^{-1}(y)$
  - 陷门：给定陷门的值k, $x=f^{-1}(y,k)$很容易计算
- 仅用于密钥管理和数字签名
- 超递增数列与陷门：简单背包$A$（超递增数列），就是由b 求解$X$的陷门
- MH背包公钥密码：超递增序列B作为私钥，选择$n \gt 2b_k$或$n\gt \sum_{j=1}^{k}{b_j}$，取$r\leq n-1$且与$n$互素；作变换 $T\equiv rB \mod n$； 作置换$P$ 得到数列$A=P*T$。仅公布陷门背包$A$
- $RSA$ ：最广泛接受的公钥方案
  - 取两个充分大的素数$p,q$
  - 计算 $n = pq(公开)$
  - 计算$\varphi(n)=(p-1)(q-1)(保密)$ 
  - 随机选取整数$e(公开)$ 满足 $gcd(e,\varphi(n))=1$
  - 计算$d(保密)$ 满足 $de\equiv 1 \mod \varphi(n)$
  - 对明文的加密算法：按长度不大于$log_2n$进行分组；$c=p^e \mod n$
  - 解密：$p=c^d \mod n$
- $RSA$可能的攻击：
  - 因数分解
  - 选择密文
  - 加密指数 $e$不要过小，$2^{16}+1$
  - 解密指数 $d>1/3 \ n^{1/4}$
  - 明文攻击 对短消息进行头尾的填充
  - 模攻击 低模攻击(n太小) 同模攻击(不要使用公同饿模$n$)
  - 执行攻击 时序攻击 能量攻击
- 安全素数：$p,q$最小为512位二进制数；$n=pq$最小为1024位二进制数；$p,q$的差要比较大；$p-1, q-1$都应当至少由一个大的素因子；$gcd(p-1, q-1)$
- 利用中国剩余定理加快$RSA$解密
- Rabin机密算法
  - 密钥生成：$p,q$作为私钥，要满足 $p\equiv 3 \mod 4, q\equiv 3 \mod 4$
  - 取 $n=pq$作为公钥
  - 加密：$c \equiv x^2 \mod n$
  - 解密 $x^2 \equiv \mod n$
  - 有$c^{\frac{p-1}2}\equiv 1 \mod p$，$c$是$\mod p $的平方剩余
- $ElGamal$密码
  - 存在严重的数据扩展，密文几乎是明文的两倍，仅用于数字签名
  - 选大素数$p$，选去私钥$x$ 选取$g$为$GF(p)$的一个生成元；计算公钥$y=g^x \mod p$
  - 加密：明文$m \lt p$，任选随机$r(1\leq r\leq p-2)$
    $C_1 \equiv g^r mod p$ $C_2 \equiv m \times y^r \mod p$ 密文$C=(C_1,C_2)$
  - 解密：$m=C_2\times (C_1^x)_{-1} \mod p$
- 椭圆曲线密码$ECC$
  - 不懂

### hash 函数与消息认证码

- 保证信息完整性：防止主动攻击，保证信息不被改变或伪造
- 信息摘要(message digist ——MD): 保证信息不被改变
- Hash函数H(M)：称为杂凑函数，或散列函数
- Hash的作用:
  - 保护数据的完整性
  - 不能用于保护数据的机密性
  - 不能用于数据的抗抵赖性
- Hash函数的要求：
  - 原像计算困难性
  - 第二原像计算困难性
  - 抗冲突性
- 攻击：寻找一对或多对碰撞 （Hash函数的安全性取决于抗碰撞攻击的能力）
  - 直接攻击：找到任意一对m和m'，使H(m)=H(m')
  - 生日攻击：
- 消息认证码
  - MAC-带密钥的Hash
  - MAC的七种使用模式
- hash函数的结构——Hash迭代
  - Markle-Damgard方案：$H_0=IV \ H_i=F(H_{i-1},M_i)$
  - 迭代函数$f$的设计
    - 基于Scratch方法构建迭代压缩函数: MD2, MD4, MD5 
    - 安全Hash算法(SHA)
  - 使用对称分组密码算法作为迭代函数:DES, 3DES, AES
    - Rabin 方案 f 可以选任意分组加密算法 
    - Davis-Meyer方案 增加前馈，明文与密文相加
    - Matyas-Meyer-Oseas 方案 明文、密钥、密文进行异或加
- 安全Hash算法 SHA-512
  - 原信息长度 $\lt2^{128}$
  - 信息填充 $|M|+|P|+128 = 0\mod 1024$
  - 填充长度$|P|=-(|M|+128)\mod 1024$
  - 以字为基本处理单元
  - 压缩函数f一共80轮
  - 每一轮的结构
  - 摘要初始化
  - 字扩展 $W_0-W_{79}$
  - 轮常数 $K_0-K_{79}$
- 欧洲Hash算法Whirlpool
  - Whirlpool的轮结构 10轮
  - 每一轮的结构（类似于AES）

### 第十三章消息认证

- 认证：实体认证（身份认证）、消息认证（接收者验证接受的消息是否真是完整）
- 认证函数
  - 消息加密型
    - 对称密钥加密
    - 非对称密钥加密
    - 非对称密钥双向加密
  - 消息认证码
    - MAC认证
    - 双对称密钥MAC
    - 双对称密钥MAC
  - Hash函数
    - 对称密钥加密
    - 对称密钥只加密Hash
    - 非对称密钥只加密Hash
    - 双密钥加密
- 认证协议：单向、双向
- 保证通信实时性：时间戳、挑战应答
- 双向认证协议--对称密钥
  - Needham/Schroeder双向认证谢协议
  - Denning双向认证协议
  - Kehn92双向认证协议
- 双向认证协议--非对称密钥
  - 一个带时间戳的双向认证协议
  - WOO92双向认证协议
- 单向认证协议
  - 对称加密
  - 公钥加密

### 第十四章数字签名

- 签名：可信的、不可伪造的、不可重用的、文件不可更改、不可抵赖
- 签名机制：签名者用自己的私钥签名，验证者用签名者的公钥验证
- 带Hash的数字签名协议:先过一层H(m)
- 保密数字签名协议：先签名后加密
- 直接数字签名、带Hash的直接签名
- 数字签名方案的安全性取决于签名者私钥的安全性、要含有时间戳
- 可仲裁数字签名协议：引入可信任的第三方X作为仲裁者
- 数字签名算法：RSA签名方案、数字签名标准DSS-DSA、椭圆曲线ECC签名方案
- RSA签名方案：和RSA一起记忆
- DAS：基于ElGamal密码（基于离散对数难度）
- 特殊的数字签名：盲签名、代理签名、MUO代理签名、基于身份的签名
- 身份认证：知道某事、拥有某事、固有某事
  - 固定口令：直接使用、使用口令Hash值
  - 一次性口令：使用口令列表、使用口令$P_i$创建口令$P_{i+1}$、使用口令$P_i$的散列创建口令$P_{i+1}$的散列
  - 挑战——应答：使用对称密码（随机数、时间戳、加密Hash代替前文的密钥$K$、双向验证）；使用非对称密码（使用A的公钥、双向验证同时使用）
- 密钥分配协议：
  - Shamir协议
  - 基于KDC（可信第三方）的会话密钥分配
  - KDC的作用：每个用户之间有一个对称密钥，只用来证明用户身份；验证之后KDC发送一个临时会话密钥，实现双方的加密通信：用户很多时KDC成为通讯瓶颈
  - 同级多重KDC、分级多重KDC
- 非对称密钥的分配：
  - 数字证书：密钥与用户身份绑定
  - 公钥基础设施PKI: 制作、办法、管理数字证书的措施，其职责为
    - 证书的发布、更新与撤销
    - 密钥的存储和升级
    - 为其他协议提供服务
    - 提供访问控制
  - 可信模式：带有根的CA树形结构

### 第十五章 密钥管理体系与设施

- 密钥的层次结构：主密钥->密钥加密密钥->会话密钥/初始密钥
- 密钥管理的生命周期：12个
- 密钥保护：基于口令、基于硬件
- 密钥协商
  - Diffie-Hellman密钥交换协议
  - Diffie-Hellman密钥预分配协议
  - 协议的弱点为中间人攻击
  - STS密钥交换协议
- PKI信任模式
  - 层次信任模式
  - 网状（分布式）信任模式
  - 混合信任模式
  - 桥接信任模式
  - 多根信任模式
  - Web信任模式
  - 以用户为中心的信任模式
- 数字证书：服务器证书、电子邮件证书、客户端个人证书
- PKI的组成：数字证书认证结构CA 数字证书注册审批结构RA 数字证书库 密钥备份和恢复系统 证书撤销处理系统CRL 应用接口系统 客户端软件
- PKI的功能11个功能
- 数字证书：一个具有认证中心签名的、包含公钥拥有者信息、公钥的文件，能提供在Internet上进行身份验证的权威性电子文档

### 第十六章 PGP

- PGP是端到端的电子邮件加密系统，对电子邮件及文件提供安全保护
- 主要功能：
  - 数字签名：DSA/ RSA, SHA1
  - 信息加密：CAST/IDEA/3-DES/AES/RSA/Diffie-Hellman
  - 数据压缩：ZIP
  - 基64转换：转为ASCII码
  - 数据分段：始行分段重组
- PGP的密钥管理：一次性会话密钥 公钥/私钥对 基于口令短语的常规密钥
- 会话密钥的产生：使用上一次的会话密钥作为输入128位密钥 输出两个64位明文，按CFB反馈链接，规程128位新密钥
- 密钥标识符的使用：三种解决方案
- 密钥环
- 公钥的管理
  - A获取公钥的方式：物理手段/电话验证/通过可信的第三方/通过可信的认证中心
  - ...
- 消息的发送与接收