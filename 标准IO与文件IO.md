好的，我来帮你把这一大段课程内容整理成一份清晰的 **Markdown 笔记**，结构简洁，便于你随时复习。按照你之前的习惯，我会保证最高级标题只有一个 
# IO

## 一、标准IO基础

### 一、应用层开发的概念

* **应用程序（Application）**：等同于手机上的 APP。
* **Linux 应用层开发**：就是在 Linux 系统上开发应用程序（APP）。
* 不同操作系统（Linux/Windows/Android/iOS）都需要应用程序来支持。

---

### 二、IO（输入输出）

* **IO 含义**：Input/Output，信息交换过程。
* **输入设备**：键盘、鼠标、USB。
* **输出设备**：显示器、网口、USB。
* **双向设备**：网口、U盘（既能输入也能输出）。

---

### 三、标准IO的概念

* 一组 **通用接口**，能在不同系统上运行。
* 基于 **“一切皆文件”** 原则：所有设备统一看作文件。
* 文件的基本操作 = **读**（输出）和 **写**（输入）。

---

### 四、一切皆文件

Linux 下的文件类型：

1. **常规文件**：磁盘上的普通文件（文本、二进制等）。
2. **目录文件**：本质是索引结构。
3. **字符设备文件**：键盘、鼠标（逐字符处理）。
4. **块设备文件**：U盘、磁盘（按块存储）。
5. **管道文件**：进程间通信用。
6. **套接字文件**：网络通信。
7. **符号链接文件**：类似 Windows 快捷方式。

---

### 五、系统调用与库函数

* **系统调用**：

  * 操作系统提供的接口，用来访问内核功能。
  * 如驱动显卡输出字符。
* **库函数**：

  * 编程语言（如 C）提供的函数，封装了系统调用。
  * 示例：`printf` → 调用 C 库函数 → 库函数再调用操作系统的系统调用。
* **作用**：

  * 库函数屏蔽了不同系统调用差异，保证 **跨平台兼容性**。

---

### 六、标准IO的缓冲机制

* **目的**：减少系统调用次数，提高效率。
* **方法**：数据先写入缓冲区，再集中写入磁盘或设备。
* **常见模式**：

  * **全缓冲**：缓冲区满才写入。1024
  * **行缓冲**：遇到换行符刷新。
  * **无缓冲**：实时写入（如标准错误流）。

---

### 七、标准输入输出流

Linux 预定义了三个标准流：

1. **标准输入流 (stdin)**：默认来自键盘。
2. **标准输出流 (stdout)**：默认输出到显示器。
3. **标准错误流 (stderr)**：输出错误信息。

---

### 八、重点知识回顾

* 应用程序 = Linux 上的 APP
* **标准IO**：跨平台、统一接口
* **文件类型**：常规文件、目录、字符设备、块设备、管道、套接字、符号链接
* **系统调用 vs 库函数**：库函数是适配层，系统调用是内核接口
* **缓冲机制**：全缓冲、行缓冲、无缓冲
* **标准流**：stdin / stdout / stderr

---

要不要我帮你再画一张 **知识框架图（思维导图风格）**，把 IO、文件类型、库函数/系统调用、标准流、缓冲机制这些关系用图整理出来？


好的，我来帮你把这一整段内容整理成一个结构化、精炼的 **Markdown 笔记**，方便你快速复习。按照你的要求，只有一个最高级标题 `##`。

---

## 二、文件的打开与关闭

### 一、文件的基本概念
- Linux 中“一切皆文件”，不仅包括常规数据文件，还包括键盘、鼠标、显示器、网口、U盘等 IO 设备。
- **文件打开**：占用资源，确保使用期间不被其他程序干扰。
- **文件关闭**：释放资源，让其他程序可以使用。

---

### 二、文件的打开
- 使用 **fopen** 函数打开文件。
- **函数原型**：
  ```c
  FILE *fopen(const char *path, const char *mode);
  ```

* **返回值**：指向 `FILE` 结构体的指针（文件流）。
* **参数**：

  * `path`：文件路径（相对路径或绝对路径）。
  * `mode`：打开文件的模式（见下表）。
* **注意**：

  * 打开失败返回 `NULL`。
  * 使用前必须判断返回值是否为空，否则可能出现空指针错误。

---

### 三、文件的关闭

* 使用 **fclose** 函数关闭文件。
* 作用：释放占用的资源，避免资源泄漏。

---

### 四、文件打开模式

| 模式     | 含义   | 特点                |
| ------ | ---- | ----------------- |
| `"r"`  | 只读   | 文件必须存在            |
| `"w"`  | 只写   | 文件不存在则创建；存在则清空内容  |
| `"a"`  | 追加写  | 文件不存在则创建；存在则在末尾追加 |
| `"r+"` | 读写   | 文件必须存在；可读写，不会清空   |
| `"w+"` | 读写   | 文件不存在则创建；存在则清空内容  |
| `"a+"` | 读写追加 | 文件不存在则创建；存在则在末尾追加 |

* **r / r+**：文件必须存在。
* **w / w+**：若文件存在，内容清空；否则新建。
* **a / a+**：写入内容总在末尾，不清空原有数据。

---

### 五、重点总结

1. **文件的打开与关闭**：打开 = 占用资源；关闭 = 释放资源。
2. **fopen 使用规则**：返回 `FILE*`，失败返回 `NULL`，必须检查。
3. **文件模式**：六种基本模式，选择时注意 **文件是否必须存在**、**是否清空内容**、**是否追加**。


。
## 三、错误处理


### 一、函数
1. **全局变量 `errno`**  
   - 系统调用/库函数失败时自动设置错误码  
   - **必须包含头文件**：`#include <errno.h>`

2. **错误输出函数**  
   | 函数         | 头文件          | 用法示例                          | 输出示例                            |
   |--------------|-----------------|-----------------------------------|-------------------------------------|
   | `perror()`   | `<stdio.h>`     | `perror("fopen");`                | `fopen: No such file or directory` |
   | `strerror()` | `<string.h>`    | `printf("%s", strerror(errno));`  | `No such file or directory`         |
   - **区别**：  
     - `perror`自动附加错误描述，适合快速输出  
     - `strerror`返回字符串，需手动组合信息，更灵活

3. **编译错误处理**  
   | 错误类型                 | 表现示例                                      | 解决方案                  |
   |--------------------------|---------------------------------------------|--------------------------|
   | `errno`未定义            | `error: 'errno' undeclared`                 | 添加`#include <errno.h>`  |
   | 隐式函数声明（如`strerror`）| `warning: implicit declaration of function`| 添加`#include <string.h>`|

---

### 二、最佳实践
1. **完整文件操作模板**  
```c
#include <stdio.h>
#include <errno.h>
#include <string.h>

FILE *fp = fopen("file.txt", "r");
if (fp == NULL) {
    // 任选一种错误输出方式（勿同时用）
    perror("fopen"); 
    // 或: printf("fopen: %s\n", strerror(errno));
    return 1;
}

// ...文件操作...

if (fclose(fp) != 0) {  // 关闭文件也需检查
    perror("fclose");
}
```

2. **高频避坑指南**  
   - 所有文件操作**必须检查返回值**（尤其`fopen`/`fclose`）  
   - `"w"`模式慎用 → 可能误删文件内容  
   - 路径分隔符：Windows用`\`或`/`，Linux用`/`（建议`/`跨平台兼容）  
   - 多线程环境避免`strerror` → 改用线程安全版`strerror_r`  

> 核心口诀：**开文件判空、读写出错查`errno`、关闭文件验返回**。




## 四、文件关闭（fclose）

### 文件关闭概念

* **文件打开**：占用系统资源，表示正在使用文件。
* **文件关闭**：归还资源，释放缓冲区，为系统和程序后续操作做准备。
* **必要性**：未关闭文件可能导致资源泄漏或数据未写入磁盘。

### fclose 函数

* **定义**：标准 IO 库函数，用于关闭文件。
* **参数**：文件指针 `FILE *fp`，必须非空。
* **返回值**：

  * 成功：返回 `0`
  * 失败：返回 `EOF`（通常为 `-1`）并设置错误号
* **缓冲区处理**：

  * 自动刷新缓冲区，将内存中未写入磁盘的数据写入文件。
  * 释放缓冲区资源。
* **程序终止**：程序结束时，所有打开的文件流会被自动关闭，无需显式调用。

### fclose 使用注意事项

* **参数非空**：传入空指针会导致程序崩溃（断错误）。
* **错误处理**：

  * 检查返回值判断关闭是否成功。
  * 使用 `perror()` 或自定义函数打印错误信息以便调试。
* **缓冲区**：

  * 不论缓冲区是否满，`fclose` 都会刷新内容写入磁盘。
  * 常规文件、打印输出等都受缓冲区机制影响。

### fclose 示例代码

```c
#include <stdio.h>

int main() {
    FILE *fp;
    int ret;

    // 打开文件
    fp = fopen("example.txt", "w");
    if (fp == NULL) {
        perror("文件打开失败");
        return -1;
    }
    printf("文件打开成功\n");

    // 写入数据
    fprintf(fp, "Hello, World!\n");

    // 关闭文件
    ret = fclose(fp);
    if (ret == 0) {
        printf("文件关闭成功\n");
    } else {
        perror("文件关闭失败");
    }

    return 0;
}
```

### 常见问题

* **调用 fclose 时文件未打开**：会出现断错误，程序崩溃。
* **忘记关闭文件**：缓冲区数据可能未写入磁盘，资源未释放。

### 课程重点

1. 文件关闭时自动刷新缓冲区并释放资源。
2. 文件关闭操作的重要性，避免资源泄漏。
3. fclose 参数必须非空，检查返回值进行错误处理。


好的，我已经根据你提供的内容，把文字整理成了**Markdown 格式**笔记，保持逻辑清晰、精简、层次分明，最高级标题只有一个 `##`，便于复习和使用：

---

## 五、单字符读写

### 1. 标准IO的打开与关闭

* 文件打开后可进行读取或写入操作，关闭文件释放资源。
* 错误处理必须加入，防止程序崩溃。
* 打开文件失败需判断返回的 `FILE*` 是否为空。

### 2. 字符输入输出概念

* 按字符读取或写入文件内容。
* 文本文件输入输出是字符输入输出的基础。

#### 2.1 字符输入函数

| 函数        | 功能          | 参数         | 返回值                      |
| --------- | ----------- | ---------- | ------------------------ |
| `fgetc`   | 从文件读取一个字符   | `FILE*` 指针 | 读取的字符（int），出错或 EOF 返回 -1 |
| `getc`    | 从标准输入读取一个字符 | `FILE*` 指针 | 与 `fgetc` 类似             |
| `getchar` | 从键盘读取一个字符   | 无          | 与 `getc(stdin)` 等效       |

* 注意：

  * `fgetc` 返回 `int` 而非 `char`，可处理有符号/无符号字符并区分 EOF。
  * 读取顺序从文件开头开始，读完一个字符，文件指针自动向后移动。
  * 文件关闭后，文件指针失效，需重新打开才能继续操作。

#### 2.2 字符输出函数

| 函数        | 功能         | 参数               | 返回值                 |
| --------- | ---------- | ---------------- | ------------------- |
| `fputc`   | 写一个字符到文件   | `char` + `FILE*` | 写入字符，出错返回 -1        |
| `putc`    | 写一个字符到标准输出 | `char` + `FILE*` | 与 `fputc` 类似        |
| `putchar` | 写一个字符到屏幕   | `char`           | 与 `putc(stdout)` 等效 |

* 注意：

  * 标准输出指针 `stdout` 为系统定义，类型为 `FILE*`。
  * 写入操作出错需判断返回值并进行错误处理。

### 3. 文件指针概念

* 文件指针记录文件当前读写位置。
* 读写操作后，指针会自动移动。
* 关闭文件后，指针失效。
* 文件读取和写入需注意文件位置，防止操作错误。
* 文件操作模式：

  * 只读 `r`：无法写入，尝试写入报错。
  * 只写 `w`：无法读取，尝试读取报错。
  * 读写 `r+`：可同时读写。
  * 追加 `a` / `a+`：写入追加到文件末尾。

### 4. 文件操作错误处理

* 打开文件失败：判断 `FILE*` 是否为空。
* 读写出错：判断函数返回值是否为 -1。
* 打开模式不正确会导致“错误的文件描述符”。

  * 只读模式写入 → 错误
  * 只写模式读取 → 错误
* 错误处理流程：

  1. 打开文件后判断是否成功。
  2. 出现错误打印信息。
  3. 关闭文件释放资源。
  4. 返回或退出，避免后续操作出错。

### 5. 示例流程（按字符读写）

1. 打开文件：

```c
FILE *fp = fopen("file.txt", "r+");
if (!fp) {
    perror("文件打开失败");
    return 0;
}
```

2. 读取一个字符：

```c
int ch = fgetc(fp);
if (ch == EOF) {
    // 错误处理
}
printf("读取字符: %c\n", ch);
```

3. 写入一个字符：

```c
int write_ch = 'w';
if (fputc(write_ch, fp) == EOF) {
    perror("写入出错");
    fclose(fp);
    return 0;
}
```

4. 关闭文件：

```c
fclose(fp);
```

### 6. 练习与注意事项

* `fgetc`、`getc`、`getchar` 用法理解，区别标准输入与文件。
* `fputc`、`putc`、`putchar` 输出到文件或屏幕。
* 文件指针读写顺序、位置移动、关闭文件后的状态。
* 文件模式与操作匹配，防止模式错误导致读写失败。
* 错误处理流程养成习惯，确保代码健壮性。
* 追加模式 `a+` 写入文件末尾，不覆盖原有内容。

---


---

## 六、按行读写

### 一、字符读写

* **概念**：标准I/O中最基本的文件操作，可以实现单个字符的读写。
* **特点**：

  1. 使用简单，无复杂坑点。
  2. 效率较低，不适合处理大量内容。

### 二、行输入输出

* **概念**：按整行进行读取或写入。
* **常用函数**：

  1. **`gets`**（已淘汰）

     * 参数：一个指向缓冲区的指针。
     * 默认从标准输入 (`stdin`) 读取，只能读取键盘输入。
     * 返回值：缓冲区指针，出错返回 `NULL`。
     * **缺点**：未指定读取大小，可能造成缓冲区溢出，安全性差。
  2. **`fgets`**

     * 参数：

       1. 缓冲区指针
       2. size：指定读取的最大字符数
       3. 文件流指针 (`FILE*`)：可从文件或标准输入读取
     * 返回值：缓冲区指针，出错返回 `NULL`
     * **特点**：

       1. 读取 `size-1` 个字符。
       2. 如果输入超过 `size`，截断并在末尾添加 `\0`。
       3. 如果输入不足 `size`，会保留换行符 `\n`。
       4. 安全性高，推荐使用。

### 三、`fgets` 使用要点

1. **缓冲区大小**：

   * 实际读取字符数 = `size - 1`
   * 超过长度会截断，末尾自动加 `\0`
   * 未满长度则会保留换行符
2. **读取来源**：

   * 可以是标准输入 (`stdin`) 或文件流 (`FILE*`)
3. **返回值检查**：

   * 若返回 `NULL`，说明读取失败，需要进行错误处理
4. **示例代码流程**：

   ```c
   #include <stdio.h>
   int main() {
       char buff[100];
       FILE *fp = fopen("test.txt", "r");
       if (!fp) {
           perror("open file failed");
           return 1;
       }
       while (fgets(buff, sizeof(buff), fp) != NULL) {
           printf("%s", buff);
       }
       fclose(fp);
       return 0;
   }
   ```

   * 可逐行读取文件内容，直到文件末尾。
   * 注意 `fgets` 读取超过缓冲区长度的行会被截断，需要循环读取。

### 四、注意事项

1. **不要使用 `gets`**

   * 已淘汰，存在缓冲区溢出风险。
2. **`fgets` 的特殊行为**

   * 输入超过 `size-1`：只保留前 `size-1` 个字符，末尾加 `\0`
   * 输入不足 `size-1`：保留换行符 `\n`，并在末尾加 `\0`
3. **错误处理**

   * 打开文件或读取失败时，应使用 `perror` 打印错误信息，保证程序健壮性。

---


## 七、按行输出

### 一、按行输出函数概述
- 常用按行输出函数有 **puts** 和 **fputs**。
- **puts**
  - 只有一个参数，用于输出字符串到标准输出（屏幕）。
  - 输出后会自动添加换行符。
  - 不支持格式化输出。
- **fputs**
  - 两个参数，第一个为字符串，第二个为输出位置（文件或标准输出）。
  - 不会自动添加换行符。
  - 可指定文件指针，如 `stdout` 输出到屏幕。

### 二、函数使用示例

#### 1. puts 使用示例
```c
#include <stdio.h>

int main() {
    int n;
    n = puts("hello world"); // 输出到屏幕
    if (n == EOF) {
        perror("puts error");
    }
    return 0;
}
````

* 成功返回非负整数，失败返回 `EOF`（通常为 -1）。
* 自动在末尾添加换行符。

#### 2. fputs 使用示例

```c
#include <stdio.h>

int main() {
    FILE *fp = fopen("output.txt", "w");
    if (!fp) {
        perror("fopen error");
        return -1;
    }

    int n = fputs("hello world", fp); // 输出到文件
    if (n == EOF) {
        perror("fputs error");
    }

    fclose(fp);
    return 0;
}
```

* 需要手动添加换行符。
* 第二个参数可为 `stdout` 输出到屏幕，或文件指针输出到文件。

### 三、文件打开模式的重要性

* 打开模式直接影响对文件操作的行为：

  * **只读模式（r）**：只能读取，不能写入。
  * **追加模式（a）**：可以在文件末尾添加数据。
  * **读写模式（r+）**：可读可写，写入从文件开头开始，会覆盖原有内容。
  * **追加读写模式（a+）**：可读可写，写入总是追加到文件末尾。
* 注意：模式选择错误可能导致写入失败或覆盖数据。

### 四、文件操作注意事项

1. **检查返回值**：puts、fputs、fopen 等函数执行后需判断返回值，防止操作失败。
2. **关闭文件**：使用 `fclose(fp)` 释放文件资源，避免文件损坏或内存泄漏。
3. **写入文件时**：确保使用合适的模式，例如想追加写入用 `a` 或 `a+`。
4. **标准输出指针**：`stdout` 可用于输出到屏幕，文件操作需使用有效的文件指针。

### 五、puts 与 fputs 区别总结

| 函数    | 参数数量 | 输出位置  | 自动换行 | 格式化 |
| ----- | ---- | ----- | ---- | --- |
| puts  | 1    | 标准输出  | 是    | 否   |
| fputs | 2    | 文件/屏幕 | 否    | 否   |

* **总结**：puts 简单方便用于屏幕输出；fputs 功能更灵活，可输出到文件或屏幕，但需手动处理换行符和错误检查。


---

## 八、二进制读写

* **`fread` / `fwrite`**

  * 通用的读写函数，既支持文本文件，也支持二进制文件。
  * 常用形式：

    ```c
    size_t fread(void *ptr, size_t size, size_t nmemb, FILE *stream);
    size_t fwrite(const void *ptr, size_t size, size_t nmemb, FILE *stream);
    ```
  * 返回实际成功读/写的块数。

* **内存管理**

  * 使用 `malloc` 动态分配缓冲区，读取完成后必须 `free`。

* **结构体内存布局**

  * 结构体在内存中是连续存储的，可整体作为二进制块写入。
  * `sizeof(struct)` 决定写入/读取的数据大小。

* **ASCII 与二进制差异**

  * 文本模式下是可见字符。
  * 二进制模式下可能出现乱码，这是正常现象。

* **常见错误**

  * 写入后立即读取 → 文件指针在末尾，读不到内容。
  * 解决方法：重新定位文件指针。


```c
#include <stdio.h>
#include <stdlib.h>

// 定义一个学生结构体
typedef struct {
    int id;
    char name[20];
    float score;
} Student;

int main() {
    FILE *fp;
    Student s1 = {1001, "Alice", 95.5};
    Student s2;

    // 1. 写入二进制文件
    fp = fopen("student.dat", "wb");  // wb: write binary
    if (fp == NULL) {
        perror("文件打开失败");
        return EXIT_FAILURE;
    }
    fwrite(&s1, sizeof(Student), 1, fp);  // 写入一个结构体
    fclose(fp);

    // 2. 从二进制文件读取
    fp = fopen("student.dat", "rb");  // rb: read binary
    if (fp == NULL) {
        perror("文件打开失败");
        return EXIT_FAILURE;
    }
    fread(&s2, sizeof(Student), 1, fp);  // 读取一个结构体
    fclose(fp);

    // 3. 打印读取的内容
    printf("ID: %d, Name: %s, Score: %.2f\n", s2.id, s2.name, s2.score);

    return 0;
}
```


---

👉 总结一句话：
**`fread/fwrite` 能直接对内存块进行文件读写，适合处理结构体和二进制数据。但必须注意文件指针位置、内存释放以及数据结构的一致性。**

---




## 九、文件指针与流

### 一、文件指针与读写问题

* 写入文件后，**文件指针在文件末尾**。
* 若立即读取 → **读不到内容**。
* 简单办法：**关闭再打开文件** → 指针回到开头。
* 但若要在 **文件中间** 读写，就需要 **文件定位函数**。

---

### 二、刷新流（fflush）

#### 缓冲区机制

* 标准IO有 **缓冲区**：

  * 缓冲区未满 或 未遇到换行 → 数据不会写入文件/终端。
  * 导致结果 **不能实时可见**。

#### fflush 函数

```c
int fflush(FILE *stream);
```

* 功能：强制将缓冲区数据写入目标（文件/终端）。
* 返回值：`0` 成功，`-1` 失败。
* ⚠ 仅对 **输出缓冲** 有效，输入缓冲会被丢弃。

#### 使用示例

```c
printf("abcdefg");    // 无换行，缓冲区未刷新
fflush(stdout);       // 强制刷新，立即输出到屏幕
```

```c
FILE *fp = fopen("log.txt", "w");
fwrite("abcdefg", 1, 7, fp);
fflush(fp);           // 写入磁盘，文件立即可见
```

✅ 常用于 **实时日志**。

---

### 三、流的定位函数

#### 1. ftell

```c
long ftell(FILE *stream);
```

* 返回当前文件指针位置（字节数）。
* **限制**：仅适用于 **2GB 以下文件**。

---

#### 2. fseek

```c
int fseek(FILE *stream, long offset, int origin);
```

* 改变文件指针位置。
* 参数说明：

  * `stream`：文件流指针
  * `offset`：偏移量（可正可负）
  * `origin`：起始位置

    * `SEEK_SET` → 文件开头
    * `SEEK_CUR` → 当前指针
    * `SEEK_END` → 文件末尾

⚠ 注意：

* 在 **a 模式**（append，追加）下，`fseek` **无效**，写入数据总在末尾。

---

#### 3. rewind

```c
void rewind(FILE *stream);
```

* 将文件指针重置到开头。
* 等价于：

```c
fseek(stream, 0, SEEK_SET);
```

---

### 四、代码示例

#### 1. 使用 fseek 修改文件内容

```c
FILE *fp = fopen("test.txt", "w+");
fwrite("abcdef", 1, 6, fp);

// 将指针向前移动 2 个字节，覆盖 ef
fseek(fp, -2, SEEK_CUR);
fwrite("VV", 1, 2, fp);

fclose(fp);
```

📄 文件结果：`abcdVV`

---

#### 2. 使用 rewind 回到开头

```c
FILE *fp = fopen("test.txt", "w+");
fwrite("abcdef", 1, 6, fp);

rewind(fp);  // 回到文件开头
fwrite("XYZ", 1, 3, fp);

fclose(fp);
```

📄 文件结果：`XYZdef`

---

#### 3. ftell 获取位置

```c
FILE *fp = fopen("test.txt", "w+");
fwrite("abcdef", 1, 6, fp);

long pos = ftell(fp); 
printf("当前指针位置: %ld\n", pos);  // 输出 6

rewind(fp);
printf("重置后位置: %ld\n", ftell(fp));  // 输出 0

fclose(fp);
```

---

### 五、重点总结

* **文件指针操作函数**：`ftell`、`fseek`、`rewind`
* **刷新流函数**：`fflush`
* **模式影响**：

  * `r`、`w` 模式下 → 定位函数可用
  * `a` 模式下 → `fseek` 无效
* **限制**：

  * 仅适用于 **2GB 以下文件**
  * 偏移量为 **有符号数**，支持正负偏移


---

## 十、格式化输出


### 二、函数分类与作用

| 函数        | 功能描述              | 输出/输入位置 |
| --------- | ----------------- | ------- |
| `printf`  | 将格式化字符串输出到屏幕      | 屏幕      |
| `sprintf` | 将格式化字符串输出到指定字符串   | 字符串     |
| `fprintf` | 将格式化字符串输出到文件      | 文件      |
| `fscanf`  | 从文件中读取格式化数据存储到变量  | 文件      |
| `sscanf`  | 从字符串中读取格式化数据存储到变量 | 字符串     |

* **返回值**：成功时返回输出的字符个数；出错时返回-1。
* `sprintf`和`fprintf`只是`printf`的变体，区别在于输出目标不同。
* `fscanf`和`sscanf`是`scanf`的变体，区别在于输入源不同。

---

### 三、函数原型

```c
// 输出
int sprintf(char *str, const char *format, ...);
int fprintf(FILE *stream, const char *format, ...);

// 输入
int fscanf(FILE *stream, const char *format, ...);
int sscanf(const char *str, const char *format, ...);
```

* `sprintf`：输出到字符串
* `fprintf`：输出到文件
* `fscanf`：从文件读取
* `sscanf`：从字符串读取

---

### 四、示例代码

##### 1. `sprintf` 使用示例

```c
##include <stdio.h>

int main() {
    char buffer[100] = {0};
    int year = 2021, month = 10, day = 1;

    sprintf(buffer, "%d-%d-%d", year, month, day); // 格式化输出到字符串
    printf("%s\n", buffer);  // 打印字符串

    return 0;
}
```

##### 2. `fprintf` 使用示例

```c
##include <stdio.h>

int main() {
    FILE *fp = fopen("f_test.txt", "w");
    int year = 2021, month = 10, day = 1;

    if (fp != NULL) {
        fprintf(fp, "%d-%d-%d\n", year, month, day); // 格式化写入文件
        fclose(fp);
    }

    return 0;
}
```

##### 3. `sscanf` 使用示例

```c
##include <stdio.h>

int main() {
    char buffer[] = "2021-10-01";
    int year, month, day;

    sscanf(buffer, "%d-%d-%d", &year, &month, &day); // 从字符串读取数据
    printf("%d %d %d\n", year, month, day);

    return 0;
}
```

##### 4. `fscanf` 使用示例

```c
##include <stdio.h>

int main() {
    FILE *fp = fopen("f_test.txt", "r");
    int year, month, day;

    if (fp != NULL) {
        fscanf(fp, "%d-%d-%d", &year, &month, &day); // 从文件读取数据
        printf("%d %d %d\n", year, month, day);
        fclose(fp);
    }

    return 0;
}
```

---

### 五、应用场景

1. **`sprintf`**：常用于字符串处理，生成格式化字符串，不需要直接打印或写入文件。
2. **`fprintf`**：适用于将格式化输出写入文件，例如日志记录。
3. **`sscanf`**：从字符串中提取指定格式的数据，例如解析输入或日志行。
4. **`fscanf`**：从文件中提取指定格式的数据，常用于文件数据分析。

> 注：在处理日志或文本文件时，通常先使用 `fgets` 读取一行，再用 `sscanf` 解析。

---

### 六、重点总结

* 输出函数：`printf` → 屏幕，`sprintf` → 字符串，`fprintf` → 文件
* 输入函数：`scanf` → 屏幕，`sscanf` → 字符串，`fscanf` → 文件
* 成功返回字符数，失败返回-1
* **最常用**：`sprintf`（字符串处理）、`sscanf`（数据解析）
* 使用输入函数时，记得对变量加 `&` 获取地址

---




## 十一、文件IO（System I/O）概述

### 一、文件IO基本概念

1. **定义**

   * 文件IO（File I/O）又称系统IO（System I/O）或系统调用（System Call）。
   * 它是操作系统提供的一组接口函数，用于对文件进行操作。

2. **文件IO vs 标准IO**

   | 特性   | 标准IO       | 文件IO（系统IO）             |
   | ---- | ---------- | ---------------------- |
   | 实现方式 | 通过库函数封装    | 直接由操作系统提供              |
   | 缓冲机制 | 提供缓冲机制     | 不提供缓冲机制，直接操作磁盘         |
   | 适用场景 | 字符串处理，频繁读写 | 二进制文件或少量读写，效率高         |
   | 数据类型 | 可处理文本或二进制  | 只提供二进制读写（包含字符串也可视作二进制） |

3. **跨平台差异**

   * 不同操作系统的文件IO接口有所差异。
   * POSIX标准：为类UNIX系统定义了一组可移植操作系统接口。Linux、Unix均实现POSIX接口，Windows实现较差。

---

### 二、文件IO特点

1. 不提供缓冲机制，直接读写磁盘。
2. 读写速度快，但频繁读写效率不如标准IO。
3. 适合只读/写一次文件的场景。

---

### 三、文件IO常用函数

| 功能   | 文件IO函数    | 标准IO对应函数             |
| ---- | --------- | -------------------- |
| 打开文件 | `open()`  | `fopen()`            |
| 关闭文件 | `close()` | `fclose()`           |
| 读取文件 | `read()`  | `fread()`/`fgets()`  |
| 写入文件 | `write()` | `fwrite()`/`fputs()` |

> 注意：文件IO只能使用对应的函数操作文件，不能与标准IO混用。

---

### 四、文件描述符（File Descriptor, FD）

1. **概念**

   * 文件描述符是文件IO操作的核心标识，用一个非负整数表示一个打开的文件。
   * 类似标准IO的文件指针（`FILE *`），但**文件描述符不是指针**，而是数字。

2. **分配规则**

   * 每个应用程序默认打开三个标准文件描述符：

     * 0：标准输入（stdin）
     * 1：标准输出（stdout）
     * 2：标准错误（stderr）
   * 用户打开的其他文件描述符从3开始分配。
   * 默认最多可打开1024个文件（0–1023）。

3. **使用示意**

   * 文件描述符类似于班级里的学号，唯一标识一个文件。
   * 文件打开时分配数字，文件关闭后数字可重复使用。

---

### 五、总结要点

1. 文件IO是操作系统提供的接口，与标准IO不同，不提供缓冲机制。
2. 文件IO适合二进制文件或少量文件操作，标准IO适合文本和频繁操作。
3. 文件IO函数：`open()`、`close()`、`read()`、`write()`
4. 文件描述符是整数标识文件：

   * 0：标准输入
   * 1：标准输出
   * 2：标准错误
   * 其他文件从3开始
5. 文件IO和标准IO不能混用，否则会出现错误。




---

---

## 十二、文件IO的open & close

| 函数            | 功能              | 常用参数                                                                 | 返回值                            | 注意点                                                                                                                                                                                                                 |
| ------------- | --------------- | -------------------------------------------------------------------- | ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **`open()`**  | 打开/创建文件，返回文件描述符 | `pathname`：文件路径  <br> `flags`：打开方式（必选）<br> `mode`：文件权限（可选，仅在创建文件时生效） | 成功：返回**非负文件描述符**<br>失败：返回 `-1` | - 文件描述符从 0 开始（0=stdin, 1=stdout, 2=stderr）<br>- `flags` 常见取值：<br> `O_RDONLY` 只读<br> `O_WRONLY` 只写<br> `O_RDWR` 读写<br> `O_CREAT` 不存在则创建<br> `O_APPEND` 追加写<br> `O_TRUNC` 打开时清空<br>- `mode` 常配合 `O_CREAT` 使用，如 `0664` |
| **`close()`** | 关闭文件，释放文件描述符    | `fd`：要关闭的文件描述符                                                       | 成功：返回 `0`<br>失败：返回 `-1`        | - 及时关闭，避免**文件描述符泄露**<br>- 关闭后 `fd` 不能再用<br>- 一般与 `open()` 配套使用                                                                                                                                                      |

---

⚡ **使用示例：**

```c
int fd = open("test.txt", O_RDWR | O_CREAT, 0664);
if (fd == -1) {
    perror("open error");
    return -1;
}

// ...读写操作...

if (close(fd) == -1) {
    perror("close error");
    return -1;
}
```

---

## 十三、文件IO读、写与定位
- 基础概念
  - 文件IO通过系统调用操作文件，核心是文件描述符 fd（整数）。
  - 常见调用：open/close、read、write、lseek。与标准IO（fopen/fread/fwrite/fseek）不通用。
  - 偏移（offset）决定下一次读写位置；lseek负责移动或查询偏移。

- 打开与关闭（open/close）
  - 常用标志：O_RDONLY / O_WRONLY / O_RDWR；O_CREAT（需mode，如0644）；O_TRUNC（清空）；O_APPEND（追加）。
  - 示例组合：O_RDWR | O_CREAT | O_APPEND, 0644（读写并在末尾追加，不清空文件）。
  - 使用完记得 close(fd)，避免资源泄漏。

- 读取（read）
  - 原型：ssize_t read(int fd, void* buf, size_t count)
  - 返回：
    - >0 实际读取字节（可能小于count，短读）
    - 0 文件结尾（EOF）
    - -1 出错（检查errno）
  - 要点：
    - 处理短读：必要时循环直到达到目标或EOF/出错。
    - 若要作为C字符串打印：最多读N-1字节，并手动补'\0'。

- 写入（write）
  - 原型：ssize_t write(int fd, const void* buf, size_t count)
  - 返回：
    - ≥0 实际写入字节（可能短写）
    - -1 出错（检查errno）
  - 要点：
    - 处理短写：循环直到全部写完。
    - O_APPEND会在每次写入前把偏移移动到文件尾。
    - 写字符串用strlen(str)；写二进制用sizeof(data)（strlen遇到'\0'会提前终止）。

- 定位（lseek）
  - 原型：off_t lseek(int fd, off_t offset, int whence)
  - whence：SEEK_SET（从头）、SEEK_CUR（从当前位置）、SEEK_END（从尾）
  - 常见用法：回到开头 lseek(fd,0,SEEK_SET)；获取大小 lseek(fd,0,SEEK_END)；查当前位置 lseek(fd,0,SEEK_CUR)
  - 大文件支持：在32位环境建议启用_FILE_OFFSET_BITS=64或使用lseek64

- 易错点与对策
  - 写后直接读返回0：偏移在文件末尾。对策：lseek(fd,0,SEEK_SET)或重新open。
  - sizeof vs strlen：
    - 错误：写字符串用sizeof(buffer)会把整个缓冲（含未初始化内容）写入。
    - 正确：字符串用strlen；二进制用sizeof。
  - 打印乱码：读入的数据未以'\0'结尾，printf会越界打印内存。对策：buf[min(nread,N-1)] = '\0'，或预先memset为0。
  - 处理EINTR与短读/短写：循环重试，直到完成或确认错误。
  - 权限与umask：O_CREAT需提供mode，最终权限受umask影响。

- 小示例（读/写/定位，尽量简洁）
```c
#include <unistd.h>
#include <fcntl.h>
#include <string.h>
#include <errno.h>
#include <stdio.h>
#include <sys/stat.h>

int main(void) {
    int fd = open("test.txt", O_RDWR | O_CREAT | O_APPEND, 0644);
    if (fd < 0) { perror("open"); return 1; }

    const char *msg = "hello, world";
    size_t len = strlen(msg);
    size_t written = 0;
    while (written < len) {
        ssize_t n = write(fd, msg + written, len - written);
        if (n < 0) {
            if (errno == EINTR) continue; // 被信号中断重试
            perror("write");
            close(fd);
            return 1;
        }
        written += (size_t)n;
    }

    // 回到文件开头再读
    if (lseek(fd, 0, SEEK_SET) == (off_t)-1) { perror("lseek"); close(fd); return 1; }

    char buf[64];
    ssize_t r = read(fd, buf, sizeof(buf) - 1); // 预留1字节给'\0'
    if (r < 0) { perror("read"); close(fd); return 1; }
    buf[(r >= 0 && r < (ssize_t)sizeof(buf)) ? r : (ssize_t)sizeof(buf) - 1] = '\0';

    printf("Read(%zd): %s\n", r, buf);

    close(fd);
    return 0;
}
```

- 速查清单
  - 写字符串：write(fd, s, strlen(s))
  - 写二进制：write(fd, &obj, sizeof(obj))
  - 读字符串安全范式：n = read(fd, buf, N-1); if (n >= 0) buf[n] = '\0';
  - 写后读：lseek(fd, 0, SEEK_SET)
  - 获取文件大小：off_t sz = lseek(fd, 0, SEEK_END); lseek(fd, 0, SEEK_SET);
  - 处理EINTR：read/write返回-1且errno==EINTR时重试


## 十四、目录
- 基本概念
  - 目录在文件系统中是“特殊文件”，需要使用专用目录API操作。
  - 遍历目录的典型三步：打开目录（opendir）→ 读取目录项（readdir 循环）→ 关闭目录（closedir）。
  - 与文件IO（open/read/close）不同：读取目录应使用 readdir，而不是 read。

- 核心API与返回约定
  - opendir(const char* name) -> DIR*
    - 成功返回目录流指针（DIR*），失败返回 NULL（检查 errno）。
  - readdir(DIR* dirp) -> struct dirent*
    - 逐项返回目录项指针；到达末尾返回 NULL。若需区分“末尾”与“错误”，循环后检查 errno（循环前将 errno 置 0）。
    - 关键字段：d_name（条目名称）。其他字段如 d_type 在部分平台上可能为 DT_UNKNOWN，需配合 stat/lstat 判断类型。
  - closedir(DIR* dirp) -> int
    - 成功返回 0，失败返回 -1（检查 errno）。
  - 头文件：#include <dirent.h>，错误处理：#include <errno.h>，输出：#include <stdio.h>，字符串：#include <string.h>

- 操作流程（要点）
  - 打开：DIR* dp = opendir("目录路径"); 判空并 perror。
  - 遍历：while ((ent = readdir(dp)) != NULL) { printf("%s\n", ent->d_name); }
    - 常见条目 . 和 ..（当前/上级目录）可在打印或递归时跳过。
  - 结束：检查 errno 以判断 readdir 是否出错；最后 closedir(dp) 释放资源。

- 易错点与对策
  - 错误把 read 当作读目录：应使用 readdir；read 针对常规文件字节流。
  - 未过滤 "." 与 ".."：递归遍历时会导致死循环或重复访问；打印时也常需跳过。
  - 忘记区分“读到末尾”与“出错”：在循环前 errno = 0；循环结束后 errno!=0 说明出错。
  - 依赖 d_type 判断类型：跨平台不可靠时用 stat/lstat 获取类型与属性。
  - 资源泄漏：异常路径记得 closedir；可用早返回前先清理。

- 示例代码（简洁遍历并跳过 "." 与 ".."）
```c
#include <dirent.h>
#include <errno.h>
#include <stdio.h>
#include <string.h>

int main(int argc, char **argv) {
    const char *path = (argc > 1) ? argv[1] : ".";
    DIR *dp = opendir(path);
    if (!dp) { perror("opendir"); return 1; }

    errno = 0;
    struct dirent *ent;
    while ((ent = readdir(dp)) != NULL) {
        const char *name = ent->d_name;
        if (strcmp(name, ".") == 0 || strcmp(name, "..") == 0) continue;
        printf("%s\n", name);
    }
    if (errno != 0) { perror("readdir"); closedir(dp); return 1; }

    if (closedir(dp) == -1) { perror("closedir"); return 1; }
    return 0;
}
```
  - 编译与运行
    - gcc -Wall -Wextra -O2 listdir.c -o listdir
    - ./listdir               # 遍历当前目录
    - ./listdir ..            # 遍历上级目录

- 速查清单
  - 打开目录：DIR *dp = opendir(path);
  - 读取项：struct dirent *e; while ((e = readdir(dp)) != NULL) { puts(e->d_name); }
  - 过滤点项：if (!strcmp(e->d_name,".") || !strcmp(e->d_name,"..")) continue;
  - 结束与错误：errno=0; 循环后 if (errno) perror("readdir");
  - 关闭目录：closedir(dp);
  - 判断类型（可选，跨平台稳妥）：使用 stat/lstat 而非仅依赖 e->d_type



## 十五、C的文件权限与文件属性
- 变更权限
  - chmod(path, mode) 与 fchmod(fd, mode)；成功返回 0，失败 -1（配合 perror/errno）。
  - 八进制模式：777=rwxrwxrwx，666=rw-rw-rw-，444=r--r--r--。
- 读取属性
  - stat 跟随符号链接；lstat 读取链接本身；fstat 由已打开的 fd 读取。
  - 结构体 struct stat 常用：st_mode（类型+权限）、st_size（字节数）、st_mtime（最近内容修改）。
  - 类型宏：S_ISREG/S_ISDIR/S_ISCHR/S_ISBLK/S_ISFIFO/S_ISSOCK/S_ISLNK。
  - 权限位宏：S_IRUSR/S_IWUSR/S_IXUSR、S_IRGRP/S_IWGRP/S_IXGRP、S_IROTH/S_IWOTH/S_IXOTH。
  - 提醒：Linux 的 st_ctime 是“状态变更”时间，非“创建时间”；创建时间需看 statx/btime 或文件系统支持。
- 时间处理
  - time_t 用 localtime 转为 struct tm；打印时：年=tm_year+1900，月=tm_mon+1。
- 环境差异提示
  - Windows 共享目录/WSL/SMB 下执行位与读位可能无法按预期修改；在原生 Linux 文件系统（如 ext4）验证最可靠。
- 编译与运行
  ```bash
  gcc -Wall -Wextra -O2 chmod_demo.c -o chmod_demo
  gcc -Wall -Wextra -O2 stat_demo.c  -o stat_demo
  ```
  ```bash
  ./chmod_demo temp 644       # 将 temp 权限改为 rw-r--r--
  ./stat_demo  chmod_demo.c   # 打印类型、权限、大小、时间
  ```

### 示例代码（课堂用）
```c name=chmod_demo.c
#include <sys/stat.h>
#include <errno.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

static void perm9(mode_t m, char out[10]) {
    out[0] = (m & S_IRUSR) ? 'r' : '-';
    out[1] = (m & S_IWUSR) ? 'w' : '-';
    out[2] = (m & S_IXUSR) ? 'x' : '-';
    out[3] = (m & S_IRGRP) ? 'r' : '-';
    out[4] = (m & S_IWGRP) ? 'w' : '-';
    out[5] = (m & S_IXGRP) ? 'x' : '-';
    out[6] = (m & S_IROTH) ? 'r' : '-';
    out[7] = (m & S_IWOTH) ? 'w' : '-';
    out[8] = (m & S_IXOTH) ? 'x' : '-';
    out[9] = '\0';
}

int main(int argc, char* argv[]) {
    if (argc != 3) {
        fprintf(stderr, "用法: %s <path> <octal_mode>\n例:  %s temp 644  或  %s temp 0755\n",
                argv[0], argv[0], argv[0]);
        return 2;
    }

    const char* path = argv[1];
    char* end = NULL;
    errno = 0;
    long mode_long = strtol(argv[2], &end, 8); // 八进制
    if (errno != 0 || end == argv[2] || mode_long < 0 || mode_long > 07777) {
        fprintf(stderr, "无效的八进制权限: %s\n", argv[2]);
        return 2;
    }

    if (chmod(path, (mode_t)mode_long) == -1) {
        fprintf(stderr, "chmod 失败: %s\n", strerror(errno));
        return 1;
    }

    // 打印结果确认
    struct stat st;
    if (stat(path, &st) == -1) {
        fprintf(stderr, "stat 失败: %s\n", strerror(errno));
        return 1;
    }

    char p[10];
    perm9(st.st_mode, p);
    printf("已将 %s 权限设置为 %04lo (%s)\n", path, (unsigned long)(st.st_mode & 07777), p);
    return 0;
}
```

```c name=stat_demo.c
#include <sys/stat.h>
#include <stdio.h>
#include <string.h>
#include <errno.h>
#include <time.h>

static char filetype_char(mode_t m) {
    if (S_ISREG(m))  return '-';
    if (S_ISDIR(m))  return 'd';
    if (S_ISCHR(m))  return 'c';
    if (S_ISBLK(m))  return 'b';
    if (S_ISFIFO(m)) return 'p';
    if (S_ISSOCK(m)) return 's';
    if (S_ISLNK(m))  return 'l';
    return '?';
}

static void perm9(mode_t m, char out[10]) {
    out[0] = (m & S_IRUSR) ? 'r' : '-';
    out[1] = (m & S_IWUSR) ? 'w' : '-';
    out[2] = (m & S_IXUSR) ? 'x' : '-';
    out[3] = (m & S_IRGRP) ? 'r' : '-';
    out[4] = (m & S_IWGRP) ? 'w' : '-';
    out[5] = (m & S_IXGRP) ? 'x' : '-';
    out[6] = (m & S_IROTH) ? 'r' : '-';
    out[7] = (m & S_IWOTH) ? 'w' : '-';
    out[8] = (m & S_IXOTH) ? 'x' : '-';
    out[9] = '\0';
}

int main(int argc, char* argv[]) {
    if (argc != 2) {
        fprintf(stderr, "用法: %s <path>\n", argv[0]);
        return 2;
    }

    const char* path = argv[1];
    struct stat st;
    if (stat(path, &st) == -1) {
        fprintf(stderr, "stat 失败: %s\n", strerror(errno));
        return 1;
    }

    // 类型 + 权限
    char perms[10];
    perm9(st.st_mode, perms);
    char t = filetype_char(st.st_mode);

    // 大小
    long long size = (long long)st.st_size;

    // 时间（到分钟）
    struct tm* tm_local = localtime(&st.st_mtime);
    if (!tm_local) {
        fprintf(stderr, "localtime 失败\n");
        return 1;
    }

    // 输出风格类似: -rw-r--r--  181  2025-08-30 16:26  filename
    printf("%c%s  %lld  %04d-%02d-%02d %02d:%02d  %s\n",
           t, perms,
           size,
           tm_local->tm_year + 1900, tm_local->tm_mon + 1, tm_local->tm_mday,
           tm_local->tm_hour, tm_local->tm_min,
           path);

    return 0;
}
```


## 十六、静态库

- 学习目标
  - 理解库、静态库与动态库的区别与适用场景
  - 掌握静态库的创建、命名规范与使用方法
  - 能定位并解决常见的链接错误（undefined reference 等）
  - 熟悉 gcc、ar 的常用选项与链接顺序要点

— 基础与概念 —
- 库（Library）
  - 已编译好的可复用二进制代码集合，供程序调用（例如标准 I/O 库、字符串库、数学库等）
  - 目的：复用功能、提升开发效率，避免每个项目重复实现通用能力
  - 操作系统相关：Linux 与 Windows 库不通用
- Linux 常见库路径
  - 系统库通常位于 /lib、/usr/lib 等目录
  - 自产库在工程目录（如当前目录 .）或自定义路径，通过 -L 指定
- 术语提示
  - 编译（compile）：把 .c 源文件变为 .o 目标文件（不做链接）
  - 链接（link）：把若干 .o 与库文件合并，生成可执行文件（或进一步生成库）

— 静态库 vs 动态库（要点对比） —
- 静态库（.a）
  - 链接时把用到的库代码拷贝进最终的可执行文件
  - 优点：运行时不依赖外部库文件；部署简单；通常启动/运行更快
  - 缺点：可执行体积变大；库升级需重新编译/链接所有依赖程序；多程序重复拷贝相同代码浪费磁盘空间
- 动态库（.so）
  - 链接时不拷贝实现，运行时加载库文件
  - 优点：节省磁盘空间、便于库独立更新
  - 缺点：程序对库存在与版本匹配存在运行依赖
- 额外提示
  - 若同名 .so 与 .a 同时存在，链接器通常优先选择 .so（除非显式设置为静态链接或仅提供 .a）

— 静态库的文件与命名规范 —
- 命名：lib<name>.a（必须以 lib 为前缀，扩展名为 .a）
  - 例：libhello.a → 链接选项写作 -lhello（不写前缀 lib 与后缀 .a）
- 组成：由一个或多个 .o 目标文件打包而成
- 头文件：对外暴露函数声明，供使用方 #include 引用（库实现文件不包含 main）

— 创建静态库：步骤与命令 —
1) 编写库实现（不含 main）
   - 例：hello.c 中实现 void hello(void);
2) 编译为目标文件（仅编译，不链接）
   - gcc -c hello.c
   - 生成 hello.o
3) 打包生成静态库（使用 ar）
   - ar -rsv libhello.a hello.o
     - r：插入/替换成员
     - s：生成符号表索引
     - v：输出详细信息
4) 查看库内容（可选）
   - ar -t libhello.a        # 列出成员
   - ar -tv libhello.a       # 含详细信息

— 使用静态库：编译与链接 —
- 在源代码中包含函数声明（或使用库提供的头文件）
  - 例：void hello(void);
- 链接命令格式
  - gcc -o <目标程序> <源文件或对象文件...> -L<库路径> -l<库名>
  - 例：gcc -o test test.c -L. -lhello
    - -L.：在当前目录查找库
    - -lhello：链接 libhello.a
- 链接顺序要点
  - 一般规则：使用者在前，依赖的库在后
  - 把目标文件/依赖上游放在 -l 之前，避免“找不到符号”的链接失败

— 常见错误与排查 —
- 报错：undefined reference to `hello`
  - 阶段：链接阶段（ld 报错，非纯编译阶段）
  - 常见原因：
    - 未链接对应库（缺少 -l 或路径 -L 错误）
    - 库名书写不当（-l 时多写了 lib 或 .a）
    - 链接顺序不当（把 -l 放在使用它的对象之前）
    - 库未正确打包（目标文件未被 ar 收入 .a）
  - 处理清单：
    - 确认有 hello.o 且已打包入 libhello.a（ar -t 检查）
    - 确认 -L 指向正确目录，-l 名称正确（不含 lib 与 .a）
    - 调整链接顺序：源/对象在前，库在后
- 报错：尝试对无 main 的源直接生成可执行
  - 现象：对库实现文件直接 gcc -o 生成可执行会失败（缺少 main）
  - 正确做法：先 gcc -c 生成 .o，再打包 .a，最终与含 main 的源文件一起链接

— 验证与工具 —
- ar -t/-tv：查看静态库包含的对象文件
- 运行验证：静态链接生成的可执行文件可独立拷贝到其它路径/机器运行（无需携带 .a）
- 体积观察：静态链接的可执行体积较大是正常现象（包含了库中用到的实现）

— 体积、升级与适用性 —
- 多程序共享：静态库会在不同可执行中产生多份拷贝，磁盘占用增加
- 升级成本：库实现更新后，所有依赖的可执行需重新编译/链接
- 适用场景：部署简洁、运行环境不可控、对启动/运行性能有要求且库更新频率不高的场合

— 实践建议与最佳实践 —
- 记忆基本命令与命名规范：lib<name>.a ↔ -l<name>
- 始终检查并明确 -L 与 -l，保持正确链接顺序
- 为库提供头文件，统一声明与实现的对外接口
- 用 ar -t 验证打包结果；必要时用 -v 观察构建细节
- 保持库的职责单一、接口稳定，便于后续维护与替换

— 最小示例：从源码到运行 —
1) 编写库实现（无 main）
```c
// hello.c
#include <stdio.h>
void hello(void) {
    printf("hello world\n");
}
```
2) 仅编译为目标文件
```bash
gcc -c hello.c            # 生成 hello.o
```
3) 打包为静态库
```bash
ar -rsv libhello.a hello.o
ar -t libhello.a          # 验证包含 hello.o
```
4) 编写使用方并链接库
```c
// test.c
void hello(void);         // 或 #include "hello.h"
int main(void) {
    hello();
    return 0;
}
```
```bash
gcc -o test test.c -L. -lhello
./test                    # 输出：hello world
```

— 参考命令速查 —
- 仅编译：gcc -c file.c
- 生成静态库：ar -rsv libname.a file1.o file2.o ...
- 查看库成员：ar -t libname.a（或 ar -tv）
- 链接可执行：gcc -o app main.c -L<path> -lname

— 可选：一键构建的最小 Makefile —
```make
# 把 libhello.a 打包并生成可执行 test
CC := gcc
AR := ar
CFLAGS := -Wall -Wextra -O2
ARFLAGS := -rsv

.PHONY: all clean
all: test

libhello.a: hello.o
	$(AR) $(ARFLAGS) $@ $^

hello.o: hello.c
	$(CC) $(CFLAGS) -c $< -o $@

test: test.c libhello.a
	$(CC) $(CFLAGS) -o $@ test.c -L. -lhello

clean:
	rm -f *.o *.a test
```


## 十七、动态库

- 学习目标
  - 理解动态库（共享库 .so）的概念、特性与适用场景
  - 掌握从源码生成动态库的完整流程与关键参数（-fPIC、-shared）
  - 正确链接与运行依赖动态库的可执行文件
  - 处理常见运行期错误（cannot open shared object file）与动态库查找路径问题
  - 熟悉 ldd 等排查工具与常见路径配置方式

— 基本概念与特性 —
- 动态库（Shared Library，Linux 扩展名 .so）
  - 多个程序在磁盘与内存中共享同一份库，实现代码复用与内存节省
  - 升级便利：替换库文件即可，通常无需重新编译应用（前提是 ABI/接口兼容）
  - 可执行文件体积较小；运行期依赖库文件存在与可达
- 与静态库的差异
  - 静态库（.a）在链接期把用到的代码复制进可执行文件；动态库在运行期由动态链接器加载
  - 静态库部署独立但体积大、升级需重链；动态库依赖库路径但易于升级

— 命名与基本规则 —
- 动态库命名：lib<name>.so（以 lib 为前缀，.so 结尾）
  - 链接选项使用 -l<name>（不要写 lib 和 .so）
  - 示例：libmyhelloby.so ↔ -lmyhelloby
- 头文件与实现
  - 头文件对外声明接口（函数原型）；库实现文件不包含 main

— 生成动态库：步骤与命令 —
1) 生成位置无关代码（PIC）
   - 目的：使代码可被加载到进程地址空间的任意位置（依赖 GOT/PLT 机制）
   - 命令：
```bash
gcc -fPIC -c hello.c
gcc -fPIC -c by.c
# 生成 hello.o、by.o（带位置无关属性）
```
2) 生成共享库（.so）
   - 通过 gcc -shared，把多个对象文件打包为动态库
```bash
gcc -shared -o libmyhelloby.so hello.o by.o
```
3) 可选：查看对象与符号
```bash
nm -C hello.o
nm -C by.o
# 可观察到与 PIC 相关的 GOT/PLT 符号条目
```

— 链接与运行：使用动态库 —
- 编写使用方程序（test.c），包含并调用库中函数
```c
// test.c
void hello(void);
void by(void);
int main(void) {
    hello();
    by();
    return 0;
}
```
- 编译与链接（开发阶段常把库放在工程目录）
```bash
gcc -o test test.c -L. -lmyhelloby
```
- 运行时库查找路径
  - 默认查找系统缓存与标准目录（/lib、/usr/lib 等），不会自动在当前目录查找
  - 若直接运行报错：
    error while loading shared libraries: libmyhelloby.so: cannot open shared object file: No such file or directory

— 解决“找不到共享库”的常用方案 —
- 方案一（不推荐用于开发堆栈混合）：把库安装进系统路径
```bash
# 推荐 /usr/local/lib（需 root），然后刷新链接器缓存
sudo cp libmyhelloby.so /usr/local/lib/
sudo ldconfig
# 或放 /usr/lib（系统路径），同样需要 ldconfig
```
- 方案二（开发/临时环境推荐）：设置环境变量 LD_LIBRARY_PATH
```bash
# 仅对当前 shell 生效
export LD_LIBRARY_PATH="$LD_LIBRARY_PATH:$(pwd)"

# 若希望所有新开 shell 都生效
echo 'export LD_LIBRARY_PATH="$LD_LIBRARY_PATH:/absolute/path/to/libdir"' >> ~/.bashrc
# 或 Zsh: ~/.zshrc
source ~/.bashrc
```
- 方案三（更稳健的可执行内嵌路径）：链接时指定 rpath（运行时库搜索路径）
```bash
# $ORIGIN 代表可执行文件所在目录，便于可执行与库的相对部署
gcc -o test test.c -L./lib -lmyhelloby -Wl,-rpath,'$ORIGIN/lib'
```
- 方案四（系统级配置，便于集中管理自定义库目录）
```bash
# 创建一个 ld.so 配置片段
echo "/opt/myapp/lib" | sudo tee /etc/ld.so.conf.d/myapp.conf
sudo ldconfig
```

— 常见错误与排查 —
- cannot open shared object file: No such file or directory
  - 含义：运行期动态链接器找不到所需 .so
  - 排查与修复：
    - 用 ldd 查看依赖解析状态与实际路径
```bash
ldd ./test
# 若显示 "not found" 则说明该库未被搜索到
```
    - 选择上述任一方案修正搜索路径（LD_LIBRARY_PATH / rpath / 安装到系统路径 + ldconfig）
- 库名/链接参数错误
  - -l 写错（不应写 lib 和 .so），-L 路径缺失，或库文件命名不规范
- 链接顺序问题
  - 一般将使用该库的对象/源文件放在前，库放在后：gcc app.o -L... -lxxx
- ABI 不兼容
  - 升级库后符号变更或 SONAME 不匹配，导致运行期找不到兼容符号

— ldd：查看可执行文件依赖的动态库 —
```bash
ldd ./test
# 输出每个依赖库及其解析到的实际路径，便于确认是否“not found”
```

— 最小示例：从源码到运行 —
1) 库实现（无 main）
```c
// hello.c
#include <stdio.h>
void hello(void) { printf("hello\n"); }

// by.c
#include <stdio.h>
void by(void) { printf("by\n"); }
```
2) 构建动态库
```bash
gcc -fPIC -c hello.c
gcc -fPIC -c by.c
gcc -shared -o libmyhelloby.so hello.o by.o
```
3) 构建并运行使用方
```bash
gcc -o test test.c -L. -lmyhelloby
# 若报找不到 .so：
export LD_LIBRARY_PATH="$LD_LIBRARY_PATH:$(pwd)"
./test
```

— 实践建议与最佳实践 —
- 开发环境优先用 LD_LIBRARY_PATH 或 -Wl,-rpath,'$ORIGIN/...'
- 生产部署建议规范化安装目录（/usr/local/lib 或专用路径 + ldconfig），并管理好库版本与 SONAME
- 保持库的接口稳定；变更对外符号需同步管理依赖应用的兼容性
- 遇到运行期加载问题，第一时间使用 ldd，并核对链接命令中的 -L/-l 与命名规范


— 可选：一键构建的最小 Makefile —
```make
CC := gcc
CFLAGS := -Wall -Wextra -O2 -fPIC
LDFLAGS := 
LIB_NAME := myhelloby
LIB_SO := lib$(LIB_NAME).so

.PHONY: all run clean

all: $(LIB_SO) test

hello.o: hello.c
	$(CC) $(CFLAGS) -c $< -o $@

by.o: by.c
	$(CC) $(CFLAGS) -c $< -o $@

$(LIB_SO): hello.o by.o
	$(CC) -shared -o $@ $^

test: test.c $(LIB_SO)
	$(CC) -o $@ test.c -L. -l$(LIB_NAME) -Wl,-rpath,'$$ORIGIN'

run: all
	./test

clean:
	rm -f *.o *.so test
```

提示
- 若希望库与可执行在同一目录使用相对路径部署，rpath 使用 $ORIGIN 是最稳妥的选择。
- 若系统级安装库，请记得运行 ldconfig 刷新链接器缓存。