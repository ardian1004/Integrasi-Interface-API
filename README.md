Integration Mapping – Sales Order Transaction (ORDERJUAL)
Overview

Project ini merupakan implementasi integrasi transaksi Sales Order antara aplikasi SFA (Sales Force Automation) dengan sistem ERP/SAP menggunakan format JSON mapping.
Tujuan utama integrasi adalah memastikan data order dari salesman dapat diterima dan diproses secara otomatis di backend ERP secara konsisten, valid, dan real-time.

Project Information
Item	Description
Project Name	Sales Order Integration
Module	ORDERJUAL
Block ID	Z01
Integration Type	API / JSON Mapping
Source System	SFA Mobile
Target System	SAP / ERP
Data Format	JSON
Transaction Type	Sales Order Header & Detail
Main Objective	Sinkronisasi transaksi order penjualan
Business Flow
Salesman Input Order
        ↓
SFA Generate JSON Payload
        ↓
Integration Middleware/API
        ↓
Validation & Mapping
        ↓
SAP/ERP Sales Order Creation
        ↓
Response Status Returned
Scope Integration

Integrasi mencakup:

Header Order
Detail Item Order
Customer Information
Delivery Information
Payment Term
Pricing & Discount
Promo Information
Branch & Salesman Mapping
JSON Structure

Struktur terdiri dari 2 bagian utama:

1. Header

Berisi informasi utama transaksi order.

Contoh field:

Field	Description	SAP Mapping
ORDERNO	Nomor Order SFA	IHREZ
CUSTNO	Customer Code	KUNNR
CUSNOTO	Ship To Customer	KUNWE
SLSNO	Salesman Code	PERNR
TGLORDER	Order Date	AUDAT
CTERM	Payment Term	ZTERM
KODECABANG	Branch Code	VKBUR
NOPO	Customer PO Number	BSTKD
ORDER_TYPE	Type Order	AUGRU
TGLKIRIM	Delivery Date	VDATU
2. Detail

Berisi item produk yang diorder.

Contoh field:

Field	Description	SAP Mapping
SEQPCODE	Item Sequence	POSNR
PCODE	Product Code	MATNR
QTY	Quantity	KWMNG
UOM	Unit of Measure	VRKME
SELLPRICE	Selling Price	KBETR
KODEDISKON	Discount Code	KSDSC
DISKONPERCENT	Discount Percent	PCDSC
DISKONVALUE	Discount Value	VADSC
KODE_PROMO	Promo Code	KSFGD
PROMOTVALUE	Promo Value	VAFGD
Validation Rules

Beberapa validasi yang diterapkan:

Mandatory Validation

Field wajib:

ORDERNO
CUSTNO
SLSNO
TGLORDER
PCODE
QTY
SELLPRICE
Default Value Handling
Field	Default Value
FLAG_NOO	N
FLAG_PROMO	N
DISKONVALUE	0
DISKONPERCENT	0
Data Type Validation
Type	Example
string	ORDERNO
number	QTY
date	TGLORDER
Technical Highlights
Features Implemented
Data Mapping

Melakukan translasi field dari SFA ke SAP field naming convention.

Mandatory Checker

Memastikan field wajib tidak kosong.

Type Validation

Validasi tipe data number/date/string.

Discount & Promo Handling

Support multiple skema discount dan promo.

Delivery Scheduling

Mendukung requested delivery date.

Branch Based Processing

Support multi cabang menggunakan KODECABANG.

Example JSON Payload
{
  "block_id": "Z01",
  "block_name": "ORDERJUAL",
  "header": {
    "ORDERNO": "SO250001",
    "CUSTNO": "C0001",
    "SLSNO": "SLS01",
    "TGLORDER": "2025-05-25",
    "CTERM": "TOP30",
    "KODECABANG": "JKT"
  },
  "details": [
    {
      "PCODE": "PRD001",
      "QTY": 10,
      "UOM": "PCS",
      "SELLPRICE": 25000
    }
  ]
}
Challenges
Complex Mapping

Field mapping harus disesuaikan dengan standar SAP naming.

Data Consistency

Menjaga sinkronisasi data antara mobile dan ERP.

Validation Accuracy

Menghindari transaksi gagal akibat data invalid.

Multi Branch Logic

Handling transaksi dari banyak cabang dan salesman.

Result & Impact
Benefits
Mengurangi input manual
Mempercepat proses order
Mengurangi human error
Real-time transaksi ke ERP
Mendukung monitoring sales order
Technical Impact
Faster order processing
Better data integrity
Easier maintenance
Scalable integration structure
Technologies Used
Technology	Usage
SQL Server	Data Processing
JSON	Payload Format
REST API	Integration Communication
SAP ERP	Target System
Middleware Integration	Data Transformation
My Role
SQL Developer / Integration Developer

Responsibilities:

Membuat mapping JSON transaksi
Menyusun validation rule
Implementasi data transformation
Optimasi query processing
Testing payload integration
Troubleshooting failed transaction
Key Achievement

✅ Berhasil membuat struktur mapping transaksi order yang scalable
✅ Mendukung integrasi multi cabang dan multi item
✅ Mengurangi kegagalan transaksi akibat invalid data
✅ Mempermudah proses monitoring dan troubleshooting integrasi ERP/SAP
