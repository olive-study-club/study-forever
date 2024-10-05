INSERT INTO TP_TR_TENDER(
    TENDER_CD,
    TENDER_DETAIL_CD,
    TENDER_MD_CD,
    TENDER_SP,
    TENDER_QTY,
    TENDER_AMT,
    CHANGE_DATE,
    NOR_CANCEL_SP,
    CARD_NO,
    CARD_APPROVE_DT,
    CARD_DEAL_ACK_NO,
    ALLOT_MM_CNT,
    CARD_CO_CD,
    CARD_VALID_YYYYMM,
    ORG_OPER_DT,
    TERMINAL_ID,
    CARD_INPUT_SP,
    APPROVAL_SP,
    ACK_VAN_CD,
    CARD_VAT_AMT,
    ELECTRO_SIGNATURE_YN,
    MD_BOND_BARCD,
    COMM_MSG_SEQ,
    CARD_COOP_SP,
    FINAL_MOD_USER_ID,
    FINAL_MOD_DTTM,
    DBL_POINT_YN,
    SAMSUNG_BASIC_POINT,
    SAMSUNG_DBL_POINT,
    SHINHAN_BASIC_POINT,
    SHINHAN_DBL_POINT,
    ATTR_C1,
    ATTR_C2,
    ATTR_C3,
    CARD_INFO_HASH,
    POINT_COOP_SP,
    POINT_COO_BASIC_POINT,
    POINT_COO_DBL_POINT,
    ETC_IMP_AMT,
    CJONE_PNT_TENDER_AMT,
    REQ_AMT,
    OPER_DT,
    ORIGIN_BIZPL_CD,
    POS_NO,
    RECEIPT_NO,
    SEQ_NO,
    BIZPL_CD) 
VALUES (
    '06',
    '12',
    NULL,
    '3',
    '0',
    '8000',
    '0',
    '1',
    '5VD98DFMKDFD993993JDKJVKD9DNDK',
    '20240721',
    NULL,
    NULL,
    NULL,
    NULL,
    NULL,
    '9818098280',
    'M',
    '0',
    '3',
    '0',
    'N',
    NULL,
    '240721201100',
    '01',
    '2910721008017',
    '2024-08-21 20:11:00',
    NULL,
    NULL,
    NULL,
    NULL,
    NULL,
    NULL,
    NULL,
    NULL,
    '20-9999-003',
    NULL,
    '0',
    '0',
    '0',
    '0',
    '0',
    '20240721',
    'D478',
    '1009',
    '00100',
    '001',
    'D478');


    INSERT INTO TP_TR_HEADER(
        OPER_DT
        , ORIGIN_BIZPL_CD
        , POS_NO
        , RECEIPT_NO
        , BIZPL_CD
        , CUST_CD
        , EMP_ID
        , RTN_EMP_ID
        , SALE_START_DT
        , SALE_END_DT
        , DEAL_SP
        , WON_CUT_AMT
        , CASH_GAP
        , TOT_AMT
        , SUSPEND_RECEIPT_NO
        , RTN_RECEIPT_NO
        , BONUS_CARD_INPUT_SP
        , BONUS_CARD_INPUT_NO
        , MEMBERSHIP_CJ_ONE_NO
        , MEMBERSHIP_OY_NO
        , RTN_REASON
        , ORG_BIZPL_CD
        , ORG_OPER_DT
        , ORG_POS_NO
        , ORG_RECEIPT_NO
        , TOT_QTY
        , GOODS_REGI_CNT
        , TENDER_REGI_CNT
        , MBR_USE_YN
        , DC_COUPON_QTY
        , EJNAL_QTY
        , PEND_CD
        , PEND_END_DT
        , PEND_BRAND
        , PEND_EMP_ID
        , CASHBILL_APPROV_YN
        , POS_SP
        , SHIFT_SEQ
        , LUCKY_NO
        , EVENT_PRT_YN
        , TAX_REFUND_AMT
        , TR_VERSION
        , SALE_HOLD_YN
        , MSS_PUR_YN
        , SELFCS_TGT_EMP_NO
        , POS_SP_DETAIL
        , DEV_IP
        , ATTR_C1
        , ATTR_C2
        , ATTR_C3
        , REGI_USER_ID
        , REGI_DTTM
        , FINAL_MOD_USER_ID
        , FINAL_MOD_DTTM
        , FRST_RECEIPT_NO
        , EXCHNG_RTN_SP
        , POS_MANUAL_DC_SP
        ) 
        VALUES (
            '20240822'
            , 'D578'
            , '1011'
            , '00049'
            , 'D578'
            , '99'
            , '2910822008017'
            , NULL
            , '2024-08-22 10:21:00'
            , '2024-08-22 10:22:44'
            , '11'
            , '0'
            , '0'
            , '100000'
            , NULL
            , NULL
            , ' '
            , NULL
            , NULL
            , NULL
            , ' '
            , NULL
            , NULL
            , NULL
            , NULL
            , '8'
            , '1'
            , '2'
            , ' '
            , '0'
            , '0'
            , ' '
            , '9999-12-31 23:59:59'
            , NULL
            , NULL
            , 2
            , ' '
            , ' '
            , ' '
            , 'N'
            , '0'
            , '8A129'
            , 'N'
            , 'N'
            , NULL
            , NULL
            , NULL
            , NULL
            , NULL
            , NULL
            , '2910822008017'
            , '2024-08-22 10:22:44'
            , '2910822008017'
            , '2024-08-22 10:22:44'
            , ' '
            , ' '
            , ' ');



