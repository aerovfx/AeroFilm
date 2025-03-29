
## Flux Gym Training Configuration

### Training Parameters

- **Repeat trains per image**: `10`
  - Mỗi hình ảnh sẽ được huấn luyện lại 10 lần để tăng cường học mẫu.

- **Max Train Epochs**: `16`
  - Mô hình sẽ huấn luyện tối đa 16 epochs (chu kỳ học).

- **Expected training steps**: `7040`
  - Số bước huấn luyện dự kiến.

- **Sample Image Prompts**: `"p3hinata"`
  - Tên prompt cho ảnh mẫu sẽ được tạo ra trong quá trình huấn luyện.

- **Sample Image Every N Steps**: `10`
  - Cứ mỗi 10 bước huấn luyện, một hình ảnh mẫu sẽ được tạo ra để kiểm tra tiến trình.

- **Resize dataset images**: `512`
  - Hình ảnh trong dataset sẽ được resize về kích thước 512x512 pixel.

### Example Images

![hinata_000840_00_20250329084247](https://github.com/user-attachments/assets/5378efd0-5f0c-4150-93f9-327de7957d72)
![hinata_000850_00_20250329085102](https://github.com/user-attachments/assets/19048d13-37be-4b56-bb87-e92e1c940089)

### Training Progress Log

```plaintext
[2025-03-29 15:21:26] [INFO] 0%|          | 0/20 [00:00<?, ?it/s]
[2025-03-29 15:21:42] [INFO] 5%|▌         | 1/20 [00:15<04:53, 15.43s/it]
[2025-03-29 15:21:58] [INFO] 10%|█         | 2/20 [00:30<04:39, 15.50s/it]
[2025-03-29 15:22:13] [INFO] 15%|█▌        | 3/20 [00:46<04:23, 15.52s/it]
[2025-03-29 15:22:29] [INFO] 20%|██        | 4/20 [01:02<04:08, 15.52s/it]
...
[2025-03-29 15:26:24] [INFO] 100%|██████████| 20/20 [05:12<00:00, 15.85s/it]
100%|██████████| 20/20 [05:12<00:00, 15.64s/it]
[2025-03-29 15:29:26] [INFO] steps:  19%|█▉        | 1330/7040 [18:14:50<78:20:23, 49.39s/it, avr_loss=0.385]
[2025-03-29 15:29:26] [INFO] steps:  19%|█▉        | 1331/7040 [18:15:07<78:17:16, 49.37s/it, avr_loss=0.385]
...
[2025-03-29 15:29:26] [INFO] steps:  19%|█▉        | 1340/7040 [18:17:40<77:49:12, 49.15s/it, avr_loss=0.386]
```
### Tổng kết qua lần train thử nghiệm với Fluxgym
Tối ưu thời gian huấn luyện
Giảm số lần lặp lại trên mỗi ảnh (Repeat trains per image)

Giá trị 10 là hơi cao, có thể giảm xuống 5-7 nếu dataset đa dạng.

Giảm số epochs nếu có overfitting

Nếu thấy model hội tụ sớm, có thể thử giảm Max Train Epochs xuống 10-12.

Tăng số bước giữa các lần tạo ảnh mẫu (Sample Image Every N Steps)

Hiện tại, cứ mỗi 10 bước lại tạo ảnh mẫu, điều này có thể làm chậm huấn luyện.

Tăng lên 50-100 bước để giảm tải.

Sử dụng batch size lớn hơn

Nếu phần cứng đủ mạnh, tăng batch size sẽ giúp giảm số bước huấn luyện cần thiết.

Dùng mixed precision training

Nếu hệ thống hỗ trợ FP16 (float16), có thể giúp tăng tốc đáng kể.

 🚀
