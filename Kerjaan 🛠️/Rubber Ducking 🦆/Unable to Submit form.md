Submitted form
```json
{
  "start_filling_at": "2024-10-14T11:36:17+0700",
  "entity_id": 8011,
  "report_date": "2024-10-14",
  "entity": "branch",
  "location": [-6.2916877619517404, 106.79988645747406],
  "answer_schema":
    {
      "section_3":
        {
          "apakahAgentSudahBertransaksiMenggunakanAfin_kVoGumVm": "sudah",
          "jikaBelumBerikanAlasanBelumMelakukanTransaksi_6FjjVoQy": "-",
        },
      "section_2":
        {
          "alasanBelumMendaftarSebagaiAgen_5W1WlxFJ": "-",
          "nomorHpYangDidaftarkanDalamAfin_2aBpLVZR": "800000000",
          "statusRegistrasiAgen_mrlkz3Sg": "sudah",
        },
      "section_4":
        {
          "fotoOutletFullTampakDepan_85I8A2N6":
            [
              "https://file.kerjaan.co.id/v1/sessions/files/ac55f453-64d4-4cf7-90c3-3dc5d6db7dab-orig.jpg",
            ],
          "catatanTambahanDariArcoOpsional_rVdllTvw": "test",
          "nomorTeleponAktifWa_tw7mRWEv": "88885121",
        },
      "skipped_answers":
        {
          "section_3":
            {
              "apakahAgentSudahBertransaksiMenggunakanAfin_kVoGumVm": true,
              "jikaBelumBerikanAlasanBelumMelakukanTransaksi_6FjjVoQy": true,
            },
          "section_4": {},
          "section_1": {},
          "section_2":
            {
              "statusRegistrasiAgen_mrlkz3Sg": true,
              "nomorHpYangDidaftarkanDalamAfin_2aBpLVZR": true,
              "alasanBelumMendaftarSebagaiAgen_5W1WlxFJ": true,
            },
        },
      "section_1":
        {
          "statusRegistrasiAfin_9iZwIPjA": "belum",
          "jenisUsaha_jHgFvxNm": "outlet_telco",
          "platformProviderUtamaYangPalingSeringDigunakanSaatIni_GTMRbrAZ": "mitra_bukalapak",
          "lokasiAgen_k7cJ5rfX": "-6.291658177388537,106.79992161691189",
          "totalRataRataTransaksiHarianPadaPlatform_81a0etmI": "<10",
          "namaOutletAgen_o52g0lVX": "test",
          "namaPemilikAgen_PJV5tecp": "test",
        },
    },
  "report_assignments_digital_form_id": 1627,
}
```

Response 
```json
{
    "detail": {
        "section_2": "'nomorHpYangDidaftarkanDalamAfin_2aBpLVZR' is a required property",
        "section_3": "'apakahAgentSudahBertransaksiMenggunakanAfin_kVoGumVm' is a required property"
    }
}
```

Question schema 
```json
{  
  "type": "object",  
  "title": "Staffinc Question Form",  
  "_version": "v2.1",  
  "properties": {  
    "section_1": {  
      "type": "object",  
      "title": "Form Visit New Agent",  
      "_version": "v2.1",  
      "required": [  
        "lokasiAgen_k7cJ5rfX",  
        "namaOutletAgen_o52g0lVX",  
        "namaPemilikAgen_PJV5tecp",  
        "jenisUsaha_jHgFvxNm",  
        "platformProviderUtamaYangPalingSeringDigunakanSaatIni_GTMRbrAZ",  
        "totalRataRataTransaksiHarianPadaPlatform_81a0etmI",  
        "statusRegistrasiAfin_9iZwIPjA"  
      ],  
      "properties": {  
        "jenisUsaha_jHgFvxNm": {  
          "type": "string",  
          "anyOf": [  
            {  
              "const": "outlet_telco",  
              "title": "Outlet Telco"  
            },  
            {  
              "const": "warung_kelontong",  
              "title": "Warung Kelontong"  
            },  
            {  
              "const": "counter_hp",  
              "title": "Counter HP"  
            },  
            {  
              "const": "agent_brilink",  
              "title": "Agent BRILINK"  
            },  
            {  
              "title": "Lainnya",  
              "_isCustomOptionValue": true  
            }  
          ],  
          "title": "Jenis Usaha",  
          "_isUniqueAnswer": false  
        },  
        "lokasiAgen_k7cJ5rfX": {  
          "type": "string",  
          "title": "Lokasi Agen",  
          "_isUniqueAnswer": false  
        },  
        "namaOutletAgen_o52g0lVX": {  
          "type": "string",  
          "title": "Nama Outlet Agen",  
          "_isUniqueAnswer": false  
        },  
        "namaPemilikAgen_PJV5tecp": {  
          "type": "string",  
          "title": "Nama Pemilik Agen/Penjaga Outlet",  
          "_isUniqueAnswer": false  
        },  
        "statusRegistrasiAfin_9iZwIPjA": {  
          "type": "string",  
          "anyOf": [  
            {  
              "const": "sudah",  
              "title": "Sudah",  
              "_sectionTargetRef": "section_2"  
            },  
            {  
              "const": "belum",  
              "title": "Belum",  
              "_sectionTargetRef": "section_4"  
            }  
          ],  
          "title": "Status Registrasi AFIN",  
          "maxItems": 10,  
          "_isUniqueAnswer": false  
        },  
        "totalRataRataTransaksiHarianPadaPlatform_81a0etmI": {  
          "type": "string",  
          "anyOf": [  
            {  
              "const": "<10",  
              "title": "<10"  
            },  
            {  
              "const": "10-30",  
              "title": "10-30"  
            },  
            {  
              "const": "31-50",  
              "title": "31-50"  
            },  
            {  
              "const": ">50",  
              "title": ">50"  
            }  
          ],  
          "title": "Total rata-rata Transaksi Harian pada platform",  
          "_isUniqueAnswer": false  
        },  
        "platformProviderUtamaYangPalingSeringDigunakanSaatIni_GTMRbrAZ": {  
          "type": "string",  
          "anyOf": [  
            {  
              "const": "dana",  
              "title": "DANA"  
            },  
            {  
              "const": "mitra_shopee",  
              "title": "Mitra Shopee"  
            },  
            {  
              "const": "agen_brilink",  
              "title": "Agen BRILINK"  
            },  
            {  
              "const": "mitra_bukalapak",  
              "title": "Mitra Bukalapak"  
            },  
            {  
              "const": "src",  
              "title": "SRC"  
            },  
            {  
              "const": "seabank",  
              "title": "Seabank"  
            },  
            {  
              "const": "agen_bni46",  
              "title": "Agen BNI46"  
            },  
            {  
              "title": "Lainnya",  
              "_isCustomOptionValue": true  
            }  
          ],  
          "title": "Platform/provider utama yang paling sering digunakan saat ini.",  
          "_isUniqueAnswer": false  
        }  
      },  
      "description": "Form ini digunakan saat proses registrasi agen baru.",  
      "_nextSectionTargetRef": "section_2"  
    },  
    "section_2": {  
      "type": "object",  
      "title": "Sudah Mendaftar AFIN",  
      "_version": "v2.1",  
      "required": [  
        "nomorHpYangDidaftarkanDalamAfin_2aBpLVZR",  
        "statusRegistrasiAgen_mrlkz3Sg",  
        "alasanBelumMendaftarSebagaiAgen_5W1WlxFJ"  
      ],  
      "properties": {  
        "statusRegistrasiAgen_mrlkz3Sg": {  
          "type": "string",  
          "anyOf": [  
            {  
              "const": "sudah",  
              "title": "Sudah",  
              "_sectionTargetRef": "section_3"  
            },  
            {  
              "const": "belum",  
              "title": "Belum",  
              "_sectionTargetRef": "section_4"  
            }  
          ],  
          "title": "Status Registrasi Agen",  
          "_isUniqueAnswer": false  
        },  
        "alasanBelumMendaftarSebagaiAgen_5W1WlxFJ": {  
          "type": "string",  
          "title": "Alasan Belum mendaftar sebagai Agen",  
          "_isUniqueAnswer": false  
        },  
        "nomorHpYangDidaftarkanDalamAfin_2aBpLVZR": {  
          "type": "string",  
          "title": "Nomor HP yang didaftarkan dalam AFIN",  
          "pattern": "^8\\d{7,12}$",  
          "maxLength": 13,  
          "minLength": 8,  
          "_isUniqueAnswer": true  
        }  
      },  
      "description": "",  
      "_nextSectionTargetRef": "section_4"  
    },  
    "section_3": {  
      "type": "object",  
      "title": "Sudah mendaftar Agen",  
      "_version": "v2.1",  
      "required": [  
        "apakahAgentSudahBertransaksiMenggunakanAfin_kVoGumVm",  
        "jikaBelumBerikanAlasanBelumMelakukanTransaksi_6FjjVoQy"  
      ],  
      "properties": {  
        "apakahAgentSudahBertransaksiMenggunakanAfin_kVoGumVm": {  
          "type": "string",  
          "anyOf": [  
            {  
              "const": "sudah",  
              "title": "Sudah"  
            },  
            {  
              "const": "belum",  
              "title": "Belum"  
            }  
          ],  
          "title": "Apakah Agent sudah bertransaksi menggunakan AFIN?",  
          "_isUniqueAnswer": false  
        },  
        "jikaBelumBerikanAlasanBelumMelakukanTransaksi_6FjjVoQy": {  
          "type": "string",  
          "title": "Jika belum, berikan alasan belum melakukan transaksi",  
          "_isUniqueAnswer": false  
        }  
      },  
      "description": "",  
      "_nextSectionTargetRef": "section_4"  
    },  
    "section_4": {  
      "type": "object",  
      "title": "General",  
      "_version": "v2.1",  
      "required": [  
        "catatanTambahanDariArcoOpsional_rVdllTvw",  
        "nomorTeleponAktifWa_tw7mRWEv",  
        "fotoOutletFullTampakDepan_85I8A2N6"  
      ],  
      "properties": {  
        "nomorTeleponAktifWa_tw7mRWEv": {  
          "type": "string",  
          "title": "Nomor Telepon Aktif (WA)",  
          "pattern": "^8\\d{7,12}$",  
          "maxLength": 13,  
          "minLength": 8,  
          "_isUniqueAnswer": false  
        },  
        "fotoOutletFullTampakDepan_85I8A2N6": {  
          "type": "array",  
          "items": {  
            "type": "string",  
            "format": "uri"  
          },  
          "title": "Foto Outlet (Full Tampak Depan)",  
          "maxItems": 5  
        },  
        "catatanTambahanDariArcoOpsional_rVdllTvw": {  
          "type": "string",  
          "title": "Catatan Tambahan dari Arco",  
          "_isUniqueAnswer": false  
        }  
      },  
      "description": "",  
      "_nextSectionTargetRef": "section_eof"  
    }  
  },  
  "description": "Dynamic form"  
}
```

# Conclusion
Issue happened due to un-removed skipped answer keys from question schema.


Attempt 1 exclude skipped unique
```json
{
	"section_1":{
		"unique_as123": ""
	},
	"section_2":{},
	"section_3":{},
	"section_4":{},
}
```