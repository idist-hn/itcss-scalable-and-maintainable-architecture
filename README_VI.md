-------------------------------------
# Bài viết mẫu: [https://www.xfive.co/blog/itcss-scalable-maintainable-css-architecture/](https://www.xfive.co/blog/itcss-scalable-maintainable-css-architecture/)
Bản tiếng việt!!
-------------------------------------
## ITCSS: kiến trúc css bảo trì và mở rộng
viết bởi Lubos Kmetko ngày 10 tháng 2, 2016 
### Tôi phải làm sao để duy trì và mở rông Css của mình? Đây là điều mà các lập trình viên front-end luôn quan tâm. ITCSS là 1 câu trả lời cho vấn đề này.

Năm ngoái, khi chúng tôi bắt đầu dự án thiết kế lại [HEROized](https://www.heroized.com/), làm mới 1 số phần của trang web [Xfive.co], chúng tôi tìm kiếm 1 kiến trúc CSS có khả năng phát triển dễ dàng và có thể bảo trì về sau.

[CSS Modules](http://www.sitepoint.com/understanding-css-modules-methodology/) là một cái gì đó mới và khá kì lạ lúc bấy giờ, và chúng tôi đã lưu ý về [Thiết kế phân tử](http://patternlab.io/) đại loại như một phân tử hoá học nhân tạo. Sau đó tôi tham gia hội thảo [Roberts’s](https://csswizardry.com/)  ITCSS vào tháng 6/2015, vấn đề của  [tạp chí mạng internet](https://www.creativebloq.com/web-design/manage-large-scale-web-projects-new-css-architecture-itcss-41514731) và ngay lập tức tôi tìm thấy giải pháp đơn giản, cách tiếp cận CSS thực tế nhất.

 ### Vậy ITCSS là gì?
 ITCSS là cụm từ viết tắt của "Inverted Triangle CSS" và nó giúp bạn tổ chức các file CSS trong dự án một cách tốt nhất mà bạn có thể **gặp phải** (không phải những vấn đề thường gặp phải) đối với CSS cụ thể như **phân vùng toàn cục, mô hình thác nước và các đối tượng cụ thể.**.
ITCSS có thể sử dụng thông qua git hoặc không thông qua git và nó tương thích với các kĩ thuật lập trình như BEM (phương thức lập trình HTML,CSS hướng modules), SMACSS (phương thức phân tích thiết kế và tổ chức CSS hướng modular và có thể mở rộng) or OOCSS (CSS hướng đối tượng).
một trong những nguyên tắc chính của ITCSS là nó phân tách mã nguồn CSS của bạn thành các phần mã (được gọi là "lớp") theo 1 mô hình có dạng tam giác ngược "Inverted Triangle":
![inverted triangle](https://other.media/wp-content/uploads/2017/01/itcss_2.png)
Các lớp trên bao gồm:
 - Settings- sử dụng với các tiền xử lý và có chứa phông chữ, định nghĩa màu sắc, v.v ...
 - Tool - toàn cục hoá sử dụng mixins và functions. Điều quan trọng là không trả ra bất kỳ CSS nào trong 2 lớp đầu tiên.
 - Generic - reset và/hoặc chuẩn hoá các styles, định nghĩa lại các khối,... Đây là layer đầu tiên có tương tác với CSS thực tế.
 - Elements - định dạng các phần tử HTML (ví dụ H1, A,...). Các thành phần này được định dạng mặc định bởi trình duyệt và  chúng ta có thể định nghĩa lại chúng ở layer này.
 - Objects - các thành phần cơ sở (class-based selectors) mà chưa được định nghĩa theo 1 khuôn mẫu cụ thể, ví dụ như các thành phần đa phương tiện chỉ được biết tới trong OOCSS.
 - Components - các thành phần UI cụ thể. Đây là nơi phần lớn công việc của chúng ta được thực hiện và các thành phần UI của chúng ta thường bao gồm các đối tượng và thành phần.

 - Utilities - các tiện ích và các lớp hỗ trợ (helper class) với khả năng ghi đè bất cứ thứ gì được đặt ở đỉnh của tam giác ví dụ như việc ẩn các lớp hỗ trợ.

Mô hình tam giác cũng cho ta biết làm cách nào để biểu diễn các định dạng bằng các đối tượng được sắp xếp khi đưa ra các CSS kết quả:từ các định dạng chung tới các định dạng rõ ràng, từ các đối tượng đặc hiệu cấp thấp đến những thành phần cụ thể hơn (nhưng vẫn không quá cụ thể) và các thành phần từ xa tới thành phần tập trung gần hơn.
![Tam giác ngược](https://other.media/wp-content/uploads/2017/01/itcss_1.png)
Cách tổ chức CSS như vậy giúp bạn tránh được những Xung đột đặc trưng và nó được biểu hiện như [một đồ thị đặc trưng](https://jonassebastianohlsson.com/specificity-graph/)
 ### Tài liệu
Cập nhật 10/27/2016: Các tạp chí net vừa tái xuất bản bài báo gốc từ phiên bản in (xem tài nguyên dưới đây).
Thông thường, tại thời điểm này tôi sẽ giới thiệu về [ITCSS webpage](https://itcss.io/) cho bạn để nghiên cứu thêm về nó. Tuy nhiên,nó không có gì tồn tại mà giống với tài liệu của mã nguồn mở này.
ITCSS vẫn còn chứa đựng 1 phần và nếu bạn muốn sử dụng nó 1 cách đầy đủ nhất,bạn phải học phần giới thiệu ban đầu trên tạp chí net. Tôi không ở đây để đánh giá ý định của tác giả (Tôi rất biết ơn anh ấy vì đã chia sẻ kiến thức của anh ấy), nhưng tôi nghĩ điều này ngăn việc ITCSS được áp dụng rộng rãi hơn (có thể là ý định).
 > Vấn đề này của ITCSS khiến nó khó áp dụng rộng rãi hơn.

Điều này không làm khó được bạn khi bạn bắt đầu sử dụng nó trong dự án của mình, nếu bạn thực sự quan tâm đến việc làm như vậy. [Tiếp cận những vấn đề cụ thể ](https://www.myfavouritemagazines.co.uk/design/net-magazine-back-issues/) trên tạp chí net để nắm được những nguyên tắc cơ bản của ITCSS, và sau đó nghiên cứu các tài nguyên trực tuyến có sẵn và các ví dụ để giúp bạn áp dụng nó trong các dự án thực tế.
### Tài nguyên
Tôi đã sử dụng ITCSS vào hơn 4 dự án (bao gồm Xfive.co) và việc nghiên cứu các tài liệu nguồn về ITCSS giúp tôi hiểu rõ hơn về nó:
 - [Manage large CSS projects with ITCSS](http://www.creativebloq.com/web-design/manage-large-css-projects-itcss-101517528) - giới thiệu về ITCSS, viết bởi Harry Roberts (bài báo ban đầu được tái bản từ bản in, thiếu là các cột ngắn hơn trên biểu đồ độ đặc hiệu và tiền xử lý)
 - [Manage large-scale web projects with new CSS architecture ITCSS](https://www.creativebloq.com/web-design/manage-large-scale-web-projects-new-css-architecture-itcss-41514731) - giới thiệu tổng quan về ITCSS  và phỏng vấn Harry Roberts
 - [Harry Roberts – Managing CSS Projects with ITCSS ](https://www.youtube.com/watch?v=1OKZOV-iLj4) - cuộc nói chuyện của Harry tại DaFED và [các slide đi kèm](https://speakerdeck.com/dafed/managing-css-projects-with-itcss)
 - [Manage large CSS projects with ITCSS](https://www.youtube.com/watch?v=hz76JIU_xB0) - một screencast cho các bài báo
 - [ITCSS Screencast code](https://github.com/itcss/itcss-netmag) -  mã nguồn từ screencast phía trên trên github.
 - [Another ITCSS project example](https://github.com/csswizardry/frcss)
 - Các bài báo tại địa chỉ csswizardry.com và đặc biệt là các bài dưới đây:
    - [BEMIT: Taking the BEM Naming Convention a Step Further](https://csswizardry.com/2015/08/bemit-taking-the-bem-naming-convention-a-step-further/)
    - [More Transparent UI Code with Namespaces](https://csswizardry.com/2015/03/more-transparent-ui-code-with-namespaces/)
    - [Immutable CSS](https://csswizardry.com/2015/03/immutable-css/)
    - [The Specificity Graph](https://csswizardry.com/2014/10/the-specificity-graph/)
 - [inuitcss](https://github.com/inuitcss/inuitcss) - framework OOCSS dựa trên ITCSS, cải tiến 1 số khái niệm và 1 số chức năng
 - [The BEMIT naming convention](http://www.jamesturneronline.net/blog/bemit-naming-convention.html)
bạn có thể xem qua [Chisel](https://github.com/xfiveco/generator-chisel/), bộ sinh Yeoman của chúng tôi dành cho các dự án front-end và WordPress, hỗ trợ ITCSS.
 ### Kinh nghiệm 
Sau đây là 1 vài quan điểm của tôi dựa trên những kĩnh nghiệm tích lũy được qua các dự án ITCSS:
 ##### Nghĩ ít hơn về việc đặt tên hay tạo mẫu vị trí
Bản chất tự nhiên của ITCSS, đặc biệt khi kết hợp với [quy ước đặt tên của BEMIT](https://csswizardry.com/2015/08/bemit-taking-the-bem-naming-convention-a-step-further/) cho phép bạn tập trung vài việc giải quyết các vấn đề front-end thay vì nghĩ về tên gọi hay định dạng các vị trí.  File main.css của Xfive.co có dạng thế này:
```
@import "settings.colors";
@import "settings.global";

@import "tools.mixins";

@import "normalize-scss/normalize.scss";
@import "generic.reset";
@import "generic.box-sizing";
@import "generic.shared";

@import "elements.headings";
@import "elements.hr";
@import "elements.forms";
@import "elements.links";
@import "elements.lists";
@import "elements.page";
@import "elements.quotes";
@import "elements.tables";

@import "objects.animations";
@import "objects.drawer";
@import "objects.list-bare";
@import "objects.media";
@import "objects.layout";
@import "objects.overlays";

@import "components.404";
@import "components.about";
@import "components.archive";
@import "components.avatars";
@import "components.blog-post";
@import "components.buttons";
@import "components.callout";
@import "components.clients";
@import "components.comments";
@import "components.contact";
@import "components.cta";
@import "components.faq";
@import "components.features";
@import "components.footer";
@import "components.forms";
@import "components.header";
@import "components.headings";
@import "components.hero";
@import "components.jobs";
@import "components.legal-nav";
@import "components.main-cta";
@import "components.main-nav";
@import "components.newsletter";
@import "components.page-title";
@import "components.pagination";
@import "components.post-teaser";
@import "components.process";
@import "components.quote-banner";
@import "components.offices";
@import "components.sec-nav";
@import "components.services";
@import "components.share-buttons";
@import "components.social-media";
@import "components.team";
@import "components.testimonials";
@import "components.topbar";
@import "components.reasons";
@import "components.wordpress";
@import "components.work-list";
@import "components.work-detail";

@import "vendor.prism";

@import "trumps.clearfix";
@import "trumps.utilities";

@import "healthcheck";
```
Ghi chú: chúng tôi sử dụng [phân chia thư mục thành các lớp layer](https://github.com/xfiveco/generator-chisel/tree/master/generators/app/templates/styles/itcss)  và tự động tải các định dạng thêm mới bằng [Chisel](https://github.com/xfiveco/generator-chisel/)
 ##### Áp dụng tính sử dụng lại của đối tượng để phát triển nhanh hơn
 Các đối tượng của ITCSS là ứng cử viên hàng đầu cho việc xây dựng thư viện các thành phần có thể sử dụng lại được nhằm phát triển front-end nhanh hơn. Các thành phần UI bao gồm các đối tượng chung và các thành phần đặc thù của dự án. Ví dụ, innuitcss làm 1 framework xây dựng trên nền ITCSS, có chứa [các thành phần đối tượng](https://github.com/inuitcss/inuitcss/tree/develop/objects) nhưng lại thuộc [duy nhất một thành phần](https://github.com/inuitcss/inuitcss/tree/develop/components)
 ##### Animations
Tôi khuyên bạn nên định nghĩa các animation chung như là các đối tượng, ví dụ như @keyframes o-fade-in trong file _objects.animations.scss, các thành phần đặc thù cho animation nên được định nghĩa trong các file thành phần tương ứng, ví dụ @keyframes c-hero-scale trong file _components.hero.scss.
 ##### Tính linh hoạt
 ITCSS rất linh hoạt trong luồng công việc cũng như các công cụ của bạn. Một trong nhưng lập trình viên của chúng tôi đã bày tỏ sự quan tâm về việc ITCSS nó đã hoàn thiện như thế nào. Nhưng sự thật là điều đó hoàn toàn phụ thuộc vào bạn - ITCSS không yêu cầu bạn phải có tất cả các lớp (chỉ  sử dụng các cái có thể cần thôi). Do vậy trong 1 cài đặt tối thiểu, bạn có thể chỉ cần 1 vài thành phần với những phần tử mẫu mặc định theo trình duyệt. Tất nhiên là điều này không thiết thực chút nào - một vài cài đặt, đặt lại và/ hay chuẩn hóa CSS được sử dụng rất nhiều vì những lợi ích của chúng.
 ##### Critical CSS (các thành phần CSS quan trọng)
ITCSS hỗ trợ rất tốt với critical CSS nhờ những tiêu chuẩn của "tam giác ngược". Các thành phần dựa trên mô hình (model) cho phép bạn tách riêng từng thành phần UI thành các thành phần logic, do đó bạn thậm chí có thể chọn từng phần critical CSS của bạn thủ công (chi tiết hơn ở trong bài viết tiếp theo)


 ##### Kích thước file và trùng lặp mẫu
 Nếu có bất kỳ mỗi mối bận tâm nào về kiến trúc như ITCSS hay đơn giản là bất kỳ thành phần nào như là kiến trúc CSS, thì kích thước file là 1 trong những điều phải quan tâm. Các thành phần sẽ đóng gói các mẫu và cho phép chúng ta tránh các xung đột CSS và ghi đè, tuy nhiên điều này cũng đồng nghĩa với việc sự lặp lại mẫu có thể thường xuyên xảy ra. Trong trường hợp này ITCSS không thể so sánh với [CSS hướng chức năng ](https://blog.colepeters.com/building-and-shipping-functional-css/). Mặt khác, nếu bạn thấy có quá nhiều sự trùng lặp về các thành phần, bạn hãy cân nhắc tới việc sử dụng các đối tượng riêng biệt.
 
### Kết luận 
Bạn không sai lầm khi sử dụng ITCSS. Nó là kết quả từ kinh nghiệm sau nhiều năm làm việc của Harry Roberts, một trong những tác giả CSS nổi tiếng nhất trên thế giới. Nếu bạn muốn đào sâu vào mã nguồn 1 chút, bạn sẽ thấy rằng đây là một kiến trúc đơn giản nhưng mô cùng mạnh mẽ, cho phép bạn tạo ra những dự án nhỏ lẫn to với CSS rất dễ mở rộng và bảo trì. 
Nhưng cũng đừng quên các vấn đề khác như [CSS hướng modules](https://github.com/css-modules/css-modules) khi bạn có thời gian.
 
 ##### Tìm hiểu thêm về ITCSS?
 - [ITCSS: sau 1 năm](https://www.xfive.co/blog/itcss-year-after/) - 5 điều về tam giác ngược CSS.
 - Tham khảo [Chisel](https://github.com/xfiveco/generator-chisel), bộ sinh Yeoman cho các dự án front-end và WordPress của chúng tôi, nó có hỗ trợ ITCSS.