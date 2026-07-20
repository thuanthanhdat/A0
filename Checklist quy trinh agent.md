# **CHECKLIST — QUẢN LÝ LỘ TRÌNH XÂY DỰNG TÀI LIỆU GIỮA CÁC TÁC NHÂN**

## **MỤC ĐÍCH**

Kiểm soát quá trình xây dựng tài liệu từ lúc còn là mô tả/ngữ nghĩa cho đến khi Codex tạo artifact thật trên Git, được kiểm tra, merge, verify, ghi bằng chứng và chuyển sang work item tiếp theo.

## **NGUYÊN TẮC VẬN HÀNH BẮT BUỘC**

1. **Giai đoạn 1 chưa có artifact thật, tuyệt đối KHÔNG dùng TRANG\_THAI.**  
2. Giai đoạn 1 chỉ tạo Proposal, phản biện, tổng hợp, đồng thuận, A0 Approval và Execution Specification.  
3. TRANG\_THAI chỉ bắt đầu dùng từ khi Codex tạo hoặc sửa file thật trong repository ở Giai đoạn 2\.  
4. **Phản biện song song:** A Review và TL Review cùng phản biện một Proposal trong cùng một lượt.  
5. **Cơ chế lọc triệt tiêu:** Author tổng hợp ở vòng sau CHỈ GIỮ nội dung chưa đồng thuận; nội dung đã đồng thuận TỰ ĐỘNG BỎ khỏi vòng tranh luận tiếp theo.  
6. **Chỉ định đường dẫn tuyệt đối:** Author bắt buộc phải khai báo chính xác target\_path trong Execution Spec. Codex cấm tự ý tìm kiếm tự do trên repository để tránh lãng phí token.  
7. **Báo cáo đường dẫn bắt buộc:** Khi Codex xuất báo cáo (Execution Report), bắt buộc phải liệt kê đầy đủ danh sách đường dẫn file tạo mới, sửa đổi và file liên quan.  
8. **Mô tả kết quả rõ ràng:** Không ghi "PASS" chung chung ở phần lý do, phải ghi rõ kết luận chuyên môn chi tiết.  
9. **Bàn giao chủ động:** Sau mỗi bước có chuyển giao trách nhiệm, tác nhân đang xử lý phải chủ động phát tin nhắn bàn giao.

## **QUY CÁCH KHỐI TIN NHẮN BÀN GIAO CHUẨN (ROLE\_ROUTING\_AND\_HANDOFF\_RULE)**

Mọi khối tin nhắn bàn giao bắt buộc gồm **đúng 5 dòng** và bắt đầu bằng nhãn định hướng chỉ định:

Plaintext

```
Gửi <Tên_Tác_Nhận_Kế_Tiếp>:
RESULT=<Enum_Chuẩn_Duy_Nhất>
REASON=<Mô_tả_chi_tiết_lý_do_bằng_tiếng_Việt>
OWNER=<Role_Duy_Nhất_Nắm_Bóng>
ACTION=<Mô_tả_chi_tiết_hành_động_cần_làm_bằng_tiếng_Việt>
NEXT=<Hướng_Đi_Chuẩn_Duy_Nhất>
```

## **1\. RA QUYẾT ĐỊNH VÀ KHÓA NGỮ NGHĨA (GIAI ĐOẠN 1\)**

> **Ghi chú:** Chưa hình thành tài liệu chính thức trên Git. CẤM dùng TRANG\_THAI. Đây là giai đoạn chốt nội dung và phạm vi trước khi giao Codex thực thi.

### **1.1. Author soạn Proposal**

* **Ai làm:** Author.  
* **Làm gì:** Soạn Proposal từ yêu cầu của A0.  
* **Làm như thế nào:** Author ghi rõ mục tiêu, phạm vi, nội dung dự kiến, dependency, in-scope, out-of-scope, rủi ro và output mong muốn.  
* **Chủ sở hữu bước tiếp theo:** A Review và TL Review.

**Tin nhắn bàn giao:**

Plaintext

```
Gửi A Review:
RESULT=PASS_BEFORE_A0_APPROVAL
REASON=Proposal đã soạn xong đầy đủ mục tiêu, phạm vi, dependency và rủi ro; sẵn sàng để phản biện song song.
OWNER=A Review
ACTION=A Review (soi governance, scope, authority, risk) và TL Review (soi kiến trúc, kỹ thuật, vận hành) cùng tiến hành phản biện Proposal; nêu rõ nội dung đồng thuận, chưa đồng thuận và blocker.
NEXT=Gửi A Review
```

### **1.2. A Review và TL Review cùng phản biện**

* **Ai làm:** A Review và TL Review.  
* **Làm gì:** Cùng phản biện một Proposal (Phản biện song song).  
* **Làm như thế nào:** A Review tập trung vào governance, scope, authority và risk. TL Review tập trung vào kiến trúc, kỹ thuật và khả năng vận hành. Mỗi bên đưa claim, blocker, refinement và giải pháp đề xuất.  
* **Chủ sở hữu bước tiếp theo:** Author.

**Tin nhắn bàn giao:**

Plaintext

```
Gửi Author:
RESULT=PASS_WITH_REFINEMENT
REASON=A Review và TL Review đã hoàn tất lượt phản biện song song, đã xác định các điểm đồng thuận và các vấn đề còn blocker/refinement.
OWNER=Author
ACTION=Author tổng hợp danh sách các vấn đề còn mở; loại bỏ hoàn toàn các phần đã đồng thuận; chỉ giữ lại các issue chưa đồng thuận để yêu cầu phản biện vòng tiếp theo.
NEXT=Gửi Author
```

### **1.3. Author tổng hợp nội dung chưa đồng thuận**

* **Ai làm:** Author.  
* **Làm gì:** Tổng hợp kết quả phản biện thành danh sách issue còn mở.  
* **Làm như thế nào:** Author loại bỏ nội dung đã đồng thuận. Chỉ giữ lại nội dung chưa đồng thuận, lý do bất đồng, tác động, mức blocker/refinement, giải pháp đề xuất và câu hỏi cần chốt.  
* **Chủ sở hữu bước tiếp theo:** A Review và TL Review (nếu còn issue) HOẶC A0 (nếu hết blocker).

**Tin nhắn bàn giao (Nếu còn Issue/Blocker):**

Plaintext

```
Gửi A Review:
RESULT=PASS_WITH_REFINEMENT
REASON=Danh sách các issue chưa đồng thuận đã được Author cô lập và tổng hợp xong; các phần đã đồng thuận đã được loại bỏ.
OWNER=A Review
ACTION=A Review và TL Review tiếp tục phản biện tập trung CHỈ trên danh sách các issue còn mở; đề xuất cách sửa để đạt hội tụ; không mở lại các phần đã đồng thuận.
NEXT=Gửi A Review
```

**Tin nhắn bàn giao (Nếu đã hết Blocker \- Sẵn sàng trình A0):**

Plaintext

```
Gửi A0:
RESULT=PASS_BEFORE_A0_APPROVAL
REASON=Tất cả các blocker kiến trúc và governance đã được giải quyết hội tụ; bản Final Synthesis đã sẵn sàng để A0 phê duyệt tối cao.
OWNER=A0
ACTION=A0 xem xét bản Final Synthesis và ra quyết định Phê duyệt (PASS) hoặc Không phê duyệt (NOT_PASS) về mặt ngữ nghĩa.
NEXT=Gửi A0
```

### **1.4. Lặp vòng phản biện đến khi đạt đồng thuận**

* **Ai làm:** Author, A Review và TL Review.  
* **Làm gì:** Lặp lại vòng phản biện chỉ trên danh sách issue còn mở.  
* **Làm như thế nào:** Mỗi vòng chỉ xử lý phần chưa đồng thuận. Khi issue đã đồng thuận thì loại khỏi vòng sau.  
* **Ghi chú:** Đồng thuận nghĩa là không còn blocker ngăn trình A0.

### **1.5. A0 Approval**

* **Ai làm:** A0.  
* **Làm gì:** Phê duyệt hoặc từ chối Final Synthesis.  
* **Làm như thế nào:** A0 đọc Final Synthesis, xem còn blocker hay không, ra quyết định phê duyệt chính thức.  
* **Chủ sở hữu bước tiếp theo:** Author.

**Tin nhắn bàn giao (Nếu A0 Phê duyệt):**

Plaintext

```
Gửi Author:
RESULT=PASS_AFTER_A0_APPROVAL
REASON=A0 đã phê duyệt chính thức quyết định ngữ nghĩa. Toàn bộ nội dung đã được khóa chặt, cấm thêm semantic mới.
OWNER=Author
ACTION=Author lập Execution Specification chi tiết (chỉ thị kỹ thuật không mập mờ, ghi rõ target_path cụ thể) để giao Codex khởi tạo/sửa tài liệu thật trên Git.
NEXT=Gửi Author
```

**Tin nhắn bàn giao (Nếu A0 Không phê duyệt):**

Plaintext

```
Gửi Author:
RESULT=NOT_PASS
REASON=A0 không phê duyệt do nội dung chưa đạt yêu cầu chiến lược hoặc còn rủi ro chưa giải quyết.
OWNER=Author
ACTION=Author chỉnh sửa proposal/synthesis theo đúng chỉ đạo của A0; nếu thay đổi ngữ nghĩa cốt lõi phải gửi lại A Review và TL Review.
NEXT=Gửi Author
```

## **2\. THỰC THI TÀI LIỆU TRÊN GIT (GIAI ĐOẠN 2\)**

### **2.1. Author lập Execution Specification**

* **Ai làm:** Author.  
* **Làm gì:** Chuyển semantic decision đã được A0 phê duyệt thành chỉ thị thực thi cho Codex.  
* **Làm như thế nào:** Author ghi rõ target\_file, target\_path (đường dẫn chuẩn cố định), document\_generation\_mode, nội dung cần tạo/sửa, forbidden\_changes, validation\_required và evidence\_required. Cấm giao lệnh mập mờ ép Codex tự tìm kiếm file.  
* **Chủ sở hữu bước tiếp theo:** Codex.

**Tin nhắn bàn giao:**

Plaintext

```
Gửi Codex:
RESULT=PASS_AFTER_A0_APPROVAL
REASON=Execution Specification đã lập xong với đầy đủ target_path chuẩn xác; đủ điều kiện để Codex thao tác trên Repository mà không cần duyệt tìm kiếm tự do.
OWNER=Codex
ACTION=Kiểm tra repository tại target_path -> Tạo/Sửa file -> Tự kiểm tra (Self-validation) -> Tạo branch -> Commit -> Push -> Mở PR -> Lập Execution Report (đính kèm đầy đủ danh sách đường dẫn FILES_CREATED, FILES_MODIFIED, RELATED_FILES) -> Dừng và báo cáo A Review.
NEXT=Gửi A Review
```

### **2.2. Codex thực thi chuỗi Git**

> Bắt đầu dùng TRANG\_THAI từ bước này vì file thật đã xuất hiện trong repository.

* **TRANG\_THAI:** TAI\_LIEU\_DA\_HINH\_THANH\_TREN\_BRANCH\_HOAC\_PR  
* **Ai làm:** Codex.  
* **Làm gì:** Thực hiện chuỗi repository execution.  
* **Làm như thế nào:** Codex đọc AGENTS.md, kiểm tra trực tiếp target\_path (cấm duyệt cây thư mục tự do), tạo/sửa file, tự kiểm tra, tạo branch, commit, push, mở PR và xuất Execution Report bao gồm:  
  1. FILES\_CREATED: Danh sách đường dẫn file tạo mới.  
  2. FILES\_MODIFIED: Danh sách đường dẫn file chỉnh sửa.  
  3. RELATED\_FILES: Danh sách đường dẫn file liên quan.  
  4. Bằng chứng Commit SHA, Blob SHA, PR link.  
* **Chủ sở hữu bước tiếp theo:** A Review (theo quy tắc bắt buộc tại Mục 14 \- ROLE\_ROUTING\_AND\_HANDOFF\_RULE).

**Tin nhắn bàn giao (Nếu Codex hoàn thành chuỗi execution):**

Plaintext

```
Gửi A Review:
RESULT=CODEX_COMPLETED
REASON=Codex đã hoàn tất thao tác trên Git; Execution Report đã đính kèm đầy đủ danh sách đường dẫn FILES_CREATED, FILES_MODIFIED, RELATED_FILES và bằng chứng commit/PR.
OWNER=Codex
ACTION=Codex báo cáo hoàn thành, cung cấp PR link, commit SHA, PR diff và danh sách đầy đủ đường dẫn file để Author tiến hành Pre-merge verification.
NEXT=Gửi A Review
```

**Tin nhắn bàn giao (Nếu Codex dừng vì gặp lỗi/sự cố):**

Plaintext

```
Gửi A Review:
RESULT=TECHNICAL_FAIL
REASON=Codex phải dừng thực thi do Spec mập mờ, sai target_path, thiếu authority, vượt scope hoặc mâu thuẫn với artifact hiện hữu trên main.
OWNER=Author
ACTION=Author kiểm tra lại lý do lỗi; tiến hành sửa Execution Specification hoặc quay lại A0 nếu cần thay đổi ngữ nghĩa.
NEXT=Gửi A Review
```

## **3\. NGHIỆM THU, BẰNG CHỨNG VÀ CHUYỂN BƯỚC (GIAI ĐOẠN 3\)**

### **3.1. Author kiểm trước merge (Pre-merge Verification)**

* **TRANG\_THAI:** DANG\_KIEM\_TRA\_PR\_TRUOC\_MERGE  
* **Ai làm:** Author.  
* **Làm gì:** Kiểm tra nội dung, scope và diff trước merge.  
* **Làm như thế nào:** Author đối chiếu Execution Specification với danh sách đường dẫn file (FILES\_CREATED, FILES\_MODIFIED, RELATED\_FILES) và PR diff trong Execution Report của Codex để đảm bảo Codex sửa đúng target\_path và không có sự thay đổi ngoài phạm vi (OUT\_OF\_SCOPE\_CHANGE \= NONE).  
* **Chủ sở hữu bước tiếp theo:** Codex.

**Tin nhắn bàn giao (Nếu PR Đạt yêu cầu để Merge):**

Plaintext

```
Gửi Codex:
RESULT=PASS_AFTER_A0_APPROVAL
REASON=PR diff và danh sách đường dẫn file báo cáo hoàn toàn khớp với target_path trong Execution Spec, đúng scope và không có out-of-scope change; đủ điều kiện merge.
OWNER=Codex
ACTION=Codex tiến hành Merge PR vào main (nếu đã có merge authority); sau đó thực hiện verify main SHA, target file status và báo cáo kết quả.
NEXT=Gửi A Review
```

**Tin nhắn bàn giao (Nếu PR Chưa đạt):**

Plaintext

```
Gửi Codex:
RESULT=TECHNICAL_FAIL
REASON=PR chưa đạt do sửa sai target_path, phát sinh file thay đổi ngoài phạm vi (out-of-scope change), sai nội dung hoặc thiếu bằng chứng evidence.
OWNER=Codex
ACTION=Codex sửa lại file trên branch theo đúng Correction Specification do Author cấp; cấm sửa ngoài phạm vi; báo cáo lại kèm danh sách đường dẫn file cập nhật.
NEXT=Gửi A Review
```

### **3.2. Codex merge và verify main**

* **TRANG\_THAI:** DA\_MERGE\_VA\_VERIFY\_MAIN HOẶC MERGE\_HOAC\_VERIFY\_BI\_CHAN  
* **Ai làm:** Codex (hoặc người có thẩm quyền merge).  
* **Làm gì:** Merge PR và xác minh trạng thái vật lý trên main.  
* **Làm như thế nào:** Merge PR. Sau khi merge, kiểm tra main commit SHA, target file status, blob SHA, target path và nội dung file thực tế trên main.  
* **Chủ sở hữu bước tiếp theo:** A Review (sau đó chuyển Author nghiệm thu).

**Tin nhắn bàn giao (Nếu Merge & Verify Main Đạt):**

Plaintext

```
Gửi A Review:
RESULT=CODEX_COMPLETED
REASON=PR đã được merge thành công vào main; đã xác minh main commit SHA, blob SHA và file status tại target_path hoàn toàn hợp lệ.
OWNER=Codex
ACTION=Báo cáo bằng chứng post-merge lên hệ thống để Author tiến hành nghiệm thu kỹ thuật lần cuối.
NEXT=Gửi A Review
```

**Tin nhắn bàn giao (Nếu Merge hoặc Verify Main Bị lỗi/chặn):**

Plaintext

```
Gửi A Review:
RESULT=TECHNICAL_FAIL
REASON=Quá trình Merge bị xung đột hoặc verify main thất bại do file status/blob SHA/main SHA không khớp.
OWNER=Author
ACTION=Author đánh giá lỗi, lập Correction Spec xử lý xung đột hoặc bổ sung authority nếu bị chặn.
NEXT=Gửi A Review
```

### **3.3. Author nghiệm thu cuối (Post-merge Verification)**

* **TRANG\_THAI:** DANG\_NGHIEM\_THU\_CUOI  
* **Ai làm:** Author.  
* **Làm gì:** Kết luận cuối cùng về quá trình thực thi.  
* **Làm như thế nào:** Author đối chiếu Execution Specification, danh sách đường dẫn file báo cáo của Codex Report và repository/main thực tế.  
* **Chủ sở hữu bước tiếp theo:** Codex (nếu không đạt) HOẶC A0 / Author (nếu đạt).

**Tin nhắn bàn giao (Nếu Thực thi KHÔNG ĐẠT):**

Plaintext

```
Gửi Codex:
RESULT=TECHNICAL_FAIL
REASON=Nghiệm thu cuối thất bại do Codex thực hiện sai/thiếu spec hoặc nội dung trên main tại target_path không khớp bằng chứng evidence.
OWNER=Codex
ACTION=Codex tiến hành sửa đổi theo đúng Correction Specification do Author phát hành; cấm mở thêm semantic mới.
NEXT=Gửi A Review
```

**Tin nhắn bàn giao (Nếu Thực thi ĐẠT & Cần A0 chỉ đạo bước tiếp):**

Plaintext

```
Gửi A0:
RESULT=PASS_AFTER_A0_APPROVAL
REASON=Execution đã hoàn tất xuất sắc, đúng target_path và được verify trên main; bước tiếp theo yêu cầu chỉ đạo chiến lược hoặc A0 Gate.
OWNER=A0
ACTION=A0 xem xét kết quả đóng work item và chỉ định Work Item tiếp theo trên lộ trình Roadmap.
NEXT=Gửi A0
```

*(Nếu Thực thi ĐẠT và KHÔNG CẦN A0, Author chủ động chuyển sang bước 3.4 để đóng Checkpoint).*

### **3.4. Author tạo Checkpoint và chuyển bước**

* **TRANG\_THAI:** CHECKPOINT\_DA\_TAO  
* **Ai làm:** Author.  
* **Làm gì:** Tạo checkpoint, ghi bằng chứng evidence và xác định work item kế tiếp.  
* **Làm như thế nào:** Author ghi rõ Work Item ID, approval reference, PR link, commit SHA, main SHA, blob SHA, target\_path list, verification result; kiểm tra successor, dependency và A0 gate.  
* **Chủ sở hữu bước tiếp theo:** A0 (nếu cần quyết định mới) HOẶC Author (nếu successor đã rõ).

**Tin nhắn bàn giao (Nếu cần A0 chỉ đạo):**

Plaintext

```
Gửi A0:
RESULT=PASS_AFTER_A0_APPROVAL
REASON=Work Item đã đóng Checkpoint bằng đầy đủ bằng chứng Git và danh sách target_path đã verify; Work Item tiếp theo cần A0 duyệt Gate hoặc hướng đi mới.
OWNER=A0
ACTION=A0 phê duyệt Work Item tiếp theo hoặc ra chỉ đạo chiến lược mới.
NEXT=Gửi A0
```

**Tin nhắn bàn giao (Nếu tự động chuyển tiếp theo Roadmap đã rõ):**

Plaintext

```
Gửi Author:
RESULT=PASS_AFTER_A0_APPROVAL
REASON=Work Item đã đóng Checkpoint thành công; Work Item kế tiếp đã được định nghĩa sẵn trên Roadmap và đủ điều kiện khởi động.
OWNER=Author
ACTION=Author khởi tạo Work Item tiếp theo và bắt đầu soạn Proposal mới từ Mục 1.1.
NEXT=Gửi Author
```

