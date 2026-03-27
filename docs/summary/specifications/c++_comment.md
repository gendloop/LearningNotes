## File

* **Required (in order)**
  * `file`
  * `brief`
  * `author`

* **Example**

```cpp
// my_class.h

/**
 * @file  my_class.h
 * @brief  file_brief
 * @warning warning
 * @note note
 * @todo todo
 * @bug  bug
 * @deprecated deprecated
 * @code{.cpp}
 * int x = -1;
 * @endcode
 * @invariant invariant
 * @pre  pre
 * @post post
 * @remark remark
 * @author  gendloop
 */
```

## Class

* **Required (in order)**
  * `brief`
  * `author`

* **Example**

```cpp
/**
 * @brief brief
 * @author author
 */
```

## Func

* **Required (in order)**
  * `brief`
  * `param`
  * `author`

```cpp
/**
 * @brief   brief
 * @param[in]  var var_brief
 * @param[out]  var var_brief
 * @return  int
 * @todo  sth. is todo
 * @bug   a bug
 * @deprecated deprecated
 * @author  gendloop
 */
```

## Var

* **Required (in order)**
  * /

* **Example**

```cpp
/**
 * @brief var_brief
 * @note var_note
 */

///< var_brief
```

## References

1. [https://www.doxygen.nl/manual/docblocks.html](https://www.doxygen.nl/manual/docblocks.html)
[Doxygen Manual_ Documenting the code.html](https://www.yuque.com/attachments/yuque/0/2023/html/22048361/1704037276096-3c391c07-37b9-43ae-8583-b132522df87d.html)
