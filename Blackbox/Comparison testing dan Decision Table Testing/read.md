# Comparison Testing dan Decision Table Testing

## Tujuan
Menguji kombinasi input username dan password pada login.

| No | Username | Password | Hasil          | Screenshot |
| -- | -------- | -------- | -------------- | ---------- |
| 1  | Benar    | Benar    | Login Berhasil |<img width="1918" height="1026" alt="image" src="https://github.com/user-attachments/assets/8263b045-a128-4eb7-9610-5405478e3181" />  |
| 2  | Benar    | Salah    | Login Gagal    | <img width="1912" height="1015" alt="image" src="https://github.com/user-attachments/assets/d4e01308-28f2-42f0-93d3-156b51887fc2" /> |    
| 3  | Salah    | Benar    | Login Gagal    | <img width="1912" height="1015" alt="image" src="https://github.com/user-attachments/assets/dcbce7f0-df52-418e-b65c-49c632b168f4" /> |
| 4  | Salah    | Salah    | Login Gagal    |<img width="1912" height="1015" alt="image" src="https://github.com/user-attachments/assets/8a8a93b2-fa40-427f-8fc7-3b4d95c6a220" /> |
| 5  | Kosong   | Kosong   | Validasi       | <img width="955" height="508" alt="image" src="https://github.com/user-attachments/assets/51d46982-8d07-4241-8eb8-61304dba4af8" /><img width="959" height="515" alt="image" src="https://github.com/user-attachments/assets/4c46504f-5971-42d6-90c0-4398b21c0813" />      |

   


## Kesimpulan
Sistem dapat membedakan kombinasi input yang valid dan tidak valid.
