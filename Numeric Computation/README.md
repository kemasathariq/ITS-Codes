# A03\_102\_Kemas Muhammad Athariq

*Tugas Program Komputasi Numerik Kelas A Kelompok 3 2025*

---

### Bahas Fungsi Main

python
A. Variables
f = input("Masukkan fungsi f(x) nya: ")
f = sympify(f)
xl = float(input("Masukkan batas bawahnya (XL): "))
xu = float(input("Masukkan batas atasnya (XU): "))
x_real = float(input("Masukkan X sebenarnya: "))
bagi_dua(xl, xu, x_real, f)

B. Cara Kerja
1. Masukkan input buat fungsinya dalam bentuk string, contoh: f = x*3 + 10*x*2 - 7*x - 196
2. Jadikan inputan fungsi tersebut menjadi operasi matematika menggunakan sympify
3. Input nilai (float) Xl, Xu, dan Xsebenarnya
4. Masuk ke sub-fungsi bagi_dua

---

### Bahas Sub-fungsi bagi_dua, Et, dan Ea

#### Fungsi error_true

python
def error_true(x_real, xr):
    return abs((x_real - xr) / x_real) * 100


1. Untuk menemukan nilai *Error True*, yang mana nilai yang didapat dibandingkan dengan nilai variabel sebenarnya

#### Fungsi error_aprox

python
def error_aprox(xr, xr_old):
    return abs((xr - xr_old) / xr) * 100 if xr != 0 else float('inf')


1. Untuk menemukan nilai *Error Aprox*, yang mana nilai yang didapat dibandingkan dengan nilai sebelumnya
2. Pastikan bahwa Xr != 0, jika tidak float('inf') karena angka 0 bisa menjadi pembagi

---

### Fungsi bagi_dua

python
def bagi_dua(xl, xu, x_real, f):
    x = symbols('x')
    xr_old = 0
    i = 0

    while True:
        xr = round((xl + xu) / 2, 2)
        f_xl = f.subs(x, xl).evalf()
        f_xr = f.subs(x, xr).evalf()

        et_value = round(error_true(x_real, xr), 2)

        if f_xl * f_xr < 0:
            xu = xr
        elif f_xl * f_xr > 0:
            xl = xr
        else:
            if i == 0:
                print(f"iterasi {i+1}: xr = {xr}, Et = {et_value}, Ea = Belum bisa dicari")
            else:
                ea_value = round(error_aprox(xr, xr_old), 2)
                print(f"iterasi {i+1}: xr = {xr}, Et = {et_value}, Ea = {ea_value}")
            break 

        if i == 0:
            print(f"iterasi {i+1}: xr = {xr}, Et = {et_value}, Ea = Belum bisa dicari")
        else:
            ea_value = round(error_aprox(xr, xr_old), 2)
            print(f"iterasi {i+1}: xr = {xr}, Et = {et_value}, Ea = {ea_value}")

        if 0 <= et_value < 1:
            break

        xr_old = xr
        i += 1


1. Ubah input fungsi f(x) yang masih berupa string jadi ekspresi matematika pakai simbol x.
2. Inisialisasi xr_old = 0 buat bantu hitung error aproksimasi (Ea) di iterasi-iterasi selanjutnya.
3. Pakai perulangan while True, dan bakal berhenti kalau nilai error true (Et) udah masuk ke range 0 sampai kurang dari 1%.
4. Hitung nilai xr dari (xl + xu) / 2, terus dibulatkan pakai round() supaya lebih rapi.
5. Nilai f(xl) dan f(xr) didapat dengan masukin nilai x ke fungsi f, terus dihitung pakai evalf().
6. Et dihitung pakai fungsi error_true(), lalu dibulatkan juga.
7. Kalau hasil kali f(xl) * f(xr) < 0, berarti akar ada di antara xl dan xr, jadi xu = xr. Kalau sebaliknya, ya xl = xr.
8. Setiap iterasi akan ditampilin, tapi khusus iterasi pertama, nilai Ea belum bisa dihitung karena belum ada xr_old.
9. Setelah itu, Ea dihitung pakai fungsi error_aprox() dengan parameter xr dan xr_old.
10. Perbarui nilai Xr_old atau Xr sebelumnya
11. Increment index

---
