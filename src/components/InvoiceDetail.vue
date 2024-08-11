<template>
    <div class="invoice-detail">
        <div class="invoice-header"></div>
        <div class="invoice-main">
            <div class="invoice-master">
                <div class="invoice-type">
                    HÓA ĐƠN GIÁ TRỊ GIA TĂNG
                </div>
                <div class="invoice-type-detail">
                    KIÊM PHIẾU XUẤT KHO
                </div>
                <div class="">
                    Liên 2: Giao cho người mua
                </div>
                <div class="invoice-date">
                    {{ formatedInvDate }}
                </div>
                <div class="master-right">
                    <div>Mẫu số: {{ invoiceData.inv_template }}</div>
                    <div>Ký hiệu: {{ invoiceData.inv_seri }}</div>
                    <div>Số: {{ invoiceData.inv_no }}</div>
                </div>
            </div>
            <div class="invoice-master-seller">
                <div class="invoice-master-seller-key">
                    <div>
                        Đơn vị bán hàng
                    </div>
                    <div>
                        Mã số thuế
                    </div>
                    <div>
                        Địa chỉ
                    </div>
                    <div>
                        Số tài khoản
                    </div>
                    <div>
                        Điện thoại
                    </div>
                    <div>
                        Email
                    </div>
                </div>
                <div class="invoice-master-seller-value">
                    <div>
                        : Đơn vị bán hàng
                    </div>
                    <div>
                        : Mã số thuế
                    </div>
                    <div>
                        : Địa chỉ
                    </div>
                    <div>
                        : Số tài khoản
                    </div>
                    <div class="two-column">
                        : Điện thoại
                        <span>Fax: </span>
                    </div>
                    <div class="two-column">
                        : Email
                        <span>Website: https://asp.misa.vn</span>
                    </div>
                </div>
            </div>
            <div class="invoice-master-seller">
                <div class="invoice-master-seller-key">
                    <div>
                        Họ tên người mua hàng
                    </div>
                    <div>
                        Tên đơn vị
                    </div>
                    <div>
                        Mã số thuế
                    </div>
                    <div>
                        Địa chỉ
                    </div>
                    <div>
                        Hình thức thanh toán
                    </div>
                </div>
                <div class="invoice-master-seller-value">
                    <div>
                        : Đơn vị bán hàng
                    </div>
                    <div>
                        : Mã số thuế
                    </div>
                    <div>
                        : Địa chỉ
                    </div>
                    <div>
                        : Số tài khoản
                    </div>
                    <div>
                        : Điện thoại
                    </div>
                </div>
            </div>
            <div class="invoice-detail-data">
                <table>
                    <thead>
                        <th v-for="(item, index) in columns" :key="index">{{ item }}</th>
                    </thead>
                    <tbody>
                        <tr style="height: 12px;">
                            <td v-for="(data, inx) in columns" :key="inx">{{ inx + 1 }}</td>
                        </tr>
                        <tr v-for="(item, index) in invoiceData.items" :key="index">
                            <td v-for="(colName, index) in columnsMapping" :key="index">{{ item[colName] }}</td>
                        </tr>
                        <tr>
                            <td style="text-align: end;" :colspan="columns.length"><span>Cộng tiền hàng</span> <span>:</span> <span>100.000.000</span> </td>
                        </tr>
                        <tr>
                            <td style="text-align: end; position: relative;" :colspan="columns.length"><span>Tiền thuế GTGT</span> <span>:</span> <span>100.000.000</span> 
                                <div style="position: absolute; top: 0; left: 0;">Thuế suất GTGT: </div>
                            </td>
                        </tr>
                        <tr>
                            <td style="text-align: end;" :colspan="columns.length"><span>Tổng tiền thanh toán</span> <span>:</span> <span>100.000.000</span> </td>
                        </tr>
                        <tr>
                            <td style="text-align: start;" :colspan="columns.length"><span>Số tiền viết bằng chữ</span> <span>:</span> <span>Một trăm triệu đồng</span> </td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
    </div>
</template>

<script>
    export default{
        name: 'InvoiceDetail',
        props:{
            invoice: {
                type: Object,
            }
        },
        computed: {
            formatedInvDate() {
                let date = this.invoice.inv_date;
                let day = String(date.getDate()).padStart(2, '0');
                let month = String(date.getMonth() + 1).padStart(2, '0'); // Months are zero-indexed
                let year = date.getFullYear();

                return `Ngày ${day} Tháng ${month} Năm ${year}`;
            }

        },
        created() {
            this.invoiceData = this.invoice;
        },
        data() {
            return {
                invoiceData: null,
                columns: ['STT', 'TÊN HÀNG HÓA DỊCH VỤ', 'ĐƠN VỊ TÍNH', 'SỐ LƯỢNG', 'ĐƠN GIÁ', 'THÀNH TIỀN'],
                columnsMapping: ['no', 'item_name', 'unit', 'quantity', 'unit_price', 'total_amout']
            }
        }
    }
</script>

<style scoped>
    .invoice-detail{
        height: 100vh;
        width: 50%;
        position: fixed;
        top: 0;
        right: 0;
        box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px;
        padding: 0 20px;
    }

    .invoice-header{
        height: 54px;
        width: 100%;
        /* border-bottom: solid #ccc 1px; */
    }

    .invoice-type{
        height: 48px;
        line-height: 48px;
        font-family: TimeNewRomanBold;
        font-size: 22px;
    }
    .invoice-type-detail{
        height: 32px;
        line-height: 32px;
        font-family: TimeNewRomanBold;
        font-size: 20px;
    }
    .invoice-master{
        border: solid #bbb 1px;
        position: relative;
    }
    .invoice-date{
        padding-bottom: 16px;
    }

    .master-right{
        position: absolute;
        right: 30px;
        top: 30px;
    }
    .master-right div{
        text-align: left;
    }

    .invoice-master-seller{
        padding: 10px;
        border: solid #bbb 1px;
        border-top: unset;
        display: flex;
    }

    .invoice-master-seller-key{
        width: 200px
    }

    .invoice-master-seller-key div, .invoice-master-seller-value div{
        text-align: left;
    }

    .two-column{
        position: relative;
    }

    .two-column span {
        position: absolute;
        left: 250px;
        white-space: nowrap;
    }

    .invoice-detail-data table{
        border: solid #bbb 1px;
        border-top: unset;
        width: 100%;
    }

    .invoice-detail-data table th{
        border-right: solid #bbb 1px;
    }

    .invoice-detail-data table th:last-child, .invoice-detail-data table tr td:last-child{
        border-right: unset !important;
    }
    .invoice-detail-data table tr td{
        border-top: solid #bbb 1px;
        border-right: solid #bbb 1px;
    }
</style>