---
layout: post
title: "Đệ quy là gì?"
date: 2019-05-31
excerpt: "Phan Long"
tags: [recursion]
comments: false
---

# Đệ quy là gì?
*Chào các bạn, do dạo này mình hơi chán nên mình sẽ viết bài hướng dẫn cho các bạn cho đỡ buồn :< Nào let's start!*
## 1. Khái niệm về đệ quy
> In order to understand recursion, one must first understand recursion.

Khái niệm **đệ quy** đối với một lập trình viên ban đầu rất khó hiểu, vì thế ta hãy xét một vài ví dụ cụ thể trước khi đi vào khái niệm hoàn chỉnh của nó!

> *Giả sử bạn đi đến phòng ngủ để thay quần áo, nhanh chóng để đi làm cho kịp giờ. Nhưng bạn thấy phòng bị khóa, và bạn biết rằng con trai 3 tuổi của mình giấu chúng trong một chiếc hộp. Mở hộp ra, bạn thấy nó bao gồm nhiều chiếc hộp con khác nữa mà bên trong chúng gồm nhiều chiếc hộp nhỏ hơn. Bạn bối rối và cần tìm cách giải quyết nhanh chóng để không bị muộn làm*

- Muốn xử lý vấn đề này, ta có 2 cách tiếp cận : "**lặp**" *(loop)* và "**đệ quy**" *(recursion)*  để tạo nên một thuật toán.
![Lặp và đệ quy](https://cdn-images-1.medium.com/max/800/1*QrQ5uFKIhK3jQSFYeRBIRg.png)

- Ở cách tiếp cận thứ nhất ta sử dụng một vòng lặp. Cho đến khi không còn chiếc hộp, bạn sẽ lấy ra 1 chiếc hộp từ đống hộp và mở nó ra. 
  - **Trường hợp 1** : Nếu bạn tìm thấy chìa khóa :v Xin chúc mừng bạn đã thành công!
  - **Trường hợp 2** : Nhưng nếu xui xẻo, bạn lại tìm thấy những chiếc hộp khác, hãy đặt vào đống hộp và làm tương tự!

> *Mình sẽ minh hoạt bằng mã giả C++ như sau, sử dụng một hàng đợi để lưu đống hộp*:

``` cpp
void look_for_key()
{
    bool ok = false;
    queue < box > pile;
    pile.push(main_box);
    while(!pile.empty())
    {
        box this = pile.front();
        pile.pop();
        for(item_in_this)
            if(is_a_key(item))ok =true,break;
            else // item is a box
                q.push(item);
        if(ok)  break;
    }
}
```
- Cách tiếp cận thứ hai, chúng ta sẽ sử dụng **đệ quy**. Luôn nhớ rằng đệ quy là một hàm gọi lại chính nó.

``` cpp
// init ok = false;
void look_for_key(box)
{
    if(ok)
        break;
    for(item_in_this)
        if(is_a_key(item))
            ok =true, break;
        else // item is a box
            look_for_key(item);
}
```
> ***Phân tích*** : Ta thấy rằng ta sẽ mở chiếc hộp ra, nếu tìm thấy chìa khóa, tất nhiên là hoàn thành! Còn nếu thấy chiếc hộp, ta sẽ thực hiện lại các thao tác y như lúc ta mở chiếc hộp ban đầu!

##### Qua ví dụ trên, phần nào các bạn đã có thể hình dung ra đệ quy là gì!

> **Đệ quy** là phương pháp sử dụng trong chương trình máy tính trong đó sử dụng một hàm gọi lại chính nó.

## 2. Cơ chế đệ quy trong tin học

Ví dụ trên có thể khiến bạn nghĩ **đệ quy** khó hiểu, không đơn giản và làm bạn nản :< Hãy cố gắng lên vì rất nhiều thuật toán sử dụng **đệ quy** trong tin học. Chúng ta sẽ xét thêm một ví dụ được ứng dụng của **đệ quy**, đó là cơ chế **stack** khi gọi các hàm

>*"Trong **khoa học máy tính**, một ngăn xếp (còn gọi là bộ xếp chồng, tiếng Anh: **stack**) là một cấu trúc dữ liệu trừu tượng hoạt động theo nguyên lý "vào sau ra trước" (Last In First Out (LIFO)"* - Wikipedia.

- **Đệ quy** thường sử dụng cơ chế stack **LIFO** - vào sau ra trước khi thực hiện gọi các hàm.
- Khi một hàm đệ quy được gọi sau, nó sẽ đặt vào đầu ngăn xếp. Tưởng tượng bạn có một chồng sách, khi đặt lên hay bỏ ra một cuốn sách, bạn luôn ưu tiên cuốn sách trên cùng.
![stack](https://visualgo.net/img/stack_illustration.png)

##### Cùng xét một ví dụ cụ thể liên quan đến *toán học*, tính giai thừa! 

Chúng ra cũng có 2 cách tiếp cận, duyệt và *đệ quy*, nhưng ở đây ta chỉ xét đến các tiếp cận về **đệ quy**! Tôi sẽ chỉ cho bạn cơ chế hoạt động của stack trong hàm gọi đệ quy! Đầu tiên, tôi sẽ viết hàm đệ quy tính giai thừa của 1 số! 

> VD: Giai thừa của 5 sẽ được tính như sau `factorial (5) =  5 * 4 * 3 * 2 * 1 = 5!`

``` cpp
int fact(int x) // factorial
{
    if(x==1) return 1;
    return fact(x-1)*x;
}
```
- Nào giờ hãy cùng xem điều gì xảy ra khi gọi hàm tính giai thừa của 3 `fact(3)`:
![illustration](https://cdn-images-1.medium.com/max/800/1*YRkMsMPRFAt8Y9BiC0QVDg.png)
