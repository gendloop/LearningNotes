## Assertions

* EXPECT_*

  Do not interrupt when encountering an error

* ASSERT_*

  Interrupt when encountering an error

* User-defined error message

  e.g. `EXPECT_EQ(x, y) << "x and y are unequal"`

## Assertions Reference

* `include <gtest/gtest.h>`
* An assertion of wide string will be translate to UTF-8

### Boolean Comparison

* suffix
  * TRUE
  * FALSE
* usage
  * ASSERT_TRUE (condition)
  * EXPECT_FALSE (condition)
* range
  * bool

### Binary Comparison

* suffix
  * $$=$$ EQ
  * $$\ne$$ NE
  * $$\lt$$ LT
  * $$\le$$ LE
  * $$\gt$$ GT
  * $$\ge$$ GE
* usage
  * EXPECT_EQ (var1, var2)
  * ASSERT_EQ (var1, var2)
* range
  * int
  * char
  * pointer

### String Comparison

* suffix
  * $$=$$ EQ
  * $$\ne$$ NE
  * $$= ignore\ case$$ CASEEQ
  * $$\ne ignore\ case$$ CASENE
  * $$\gt $$ GT
  * $$\ge $$ GE
* usage
  * EXPECT_STREQ (str1, str2)
  * ASSERT_STREQ (str1, str2)
* range
  * char*
  * wchar_t*

### Float&Double Comparison

* suffix
  * $$=$$ EQ
  * $$\le abs\_error$ NEAR
* usage
  * EXPECT_FLOAT_EQ (var1, var2)
  * EXPECT_NEAR (var1, var2, abs_err)
* range
  * float
  * double
  * int

## Test Fixture

* purpose
  * share variables and configurations
* usage

```cpp
class C : public ::testing::Test {
protected:
 void SetUp() override;
 void TearDown() override;
}
TEST_F(C, case_name) {
    // details..
}
```

## Main

```cpp
int main(int argc, char** argv) {
  testing::InitGoogleTest(&argc, argv);
  GTEST_FLAG_SET(death_test_style, "fast");
  return RUN_ALL_TESTS();
}
```

## Reference

1. [Googletest Primer](https://google.github.io/googletest/primer.html)
[GoogleTest Primer _ GoogleTest.html](https://www.yuque.com/attachments/yuque/0/2023/html/22048361/1704035791667-ee6c220b-77d6-42d8-859f-343ebcb8adc3.html)
2. [Advanced GoogleTest Topics _ GoogleTest.html](https://www.yuque.com/attachments/yuque/0/2023/html/22048361/1704035822615-85e4adc9-3dd5-4c44-a1c2-bcf8a7e6fe2c.html)
3. [gMock for Dummies _ GoogleTest.html](https://www.yuque.com/attachments/yuque/0/2023/html/22048361/1704035927845-033455ad-e530-4dfd-b600-8cc9cbe0a8f7.html)
4. [Advanced GoogleTest Topics _ GoogleTest.html](https://www.yuque.com/attachments/yuque/0/2023/html/22048361/1704035939168-e8389de3-40e0-4995-95bc-a5a9bb66235e.html)
5. [gMock Cheat Sheet _ GoogleTest.html](https://www.yuque.com/attachments/yuque/0/2023/html/22048361/1704035969557-86baf3ea-8ac7-478a-8dd1-e84e8541d1af.html)
