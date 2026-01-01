import streamlit as st

# Pengaturan Judul Halaman
st.set_page_config(page_title="Kalkulator ppm & ppb", page_icon="🧪")

st.title("🧪 Kalkulator Konsentrasi & Konversi")
st.write("Alat bantu untuk menghitung ppm, ppb, dan konversi satuan konsentrasi.")

# Membuat Tab untuk navigasi
tab1, tab2 = st.tabs(["Hitung Konsentrasi", "Konversi Satuan"])

with tab1:
    st.header("Hitung ppm / ppb")
    st.write("Rumus: $ppm = \\frac{massa (mg)}{volume (L)}$")
    
    # Input dari pengguna
    massa = st.number_input("Masukkan Massa Zat Terlarut (mg)", min_value=0.0, step=0.1)
    volume = st.number_input("Masukkan Volume Pelarut (L)", min_value=0.01, step=0.1)
    
    if st.button("Hitung"):
        if volume > 0:
            ppm = massa / volume
            ppb = ppm * 1000
            
            # Menampilkan hasil
            st.success(f"Hasil Perhitungan:")
            col1, col2 = st.columns(2)
            col1.metric("Konsentrasi (ppm)", f"{ppm:.4f} mg/L")
            col2.metric("Konsentrasi (ppb)", f"{ppb:.2f} µg/L")
        else:
            st.error("Volume tidak boleh nol!")

with tab2:
    st.header("Konversi ppm ↔ ppb")
    
    mode = st.radio("Pilih Mode Konversi:", ["ppm ke ppb", "ppb ke ppm"])
    nilai_input = st.number_input("Masukkan Nilai:", min_value=0.0, step=1.0)
    
    if mode == "ppm ke ppb":
        hasil = nilai_input * 1000
        st.info(f"Hasil: **{hasil:,.2f} ppb**")
    else:
        hasil = nilai_input / 1000
        st.info(f"Hasil: **{hasil:,.6f} ppm**")

# Footer
st.markdown("---")
st.caption("Dibuat dengan Streamlit • 1 ppm = 1 mg/L • 1 ppb = 1 µg/L")
