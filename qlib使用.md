python scripts/get_data.py qlib_data --target_dir D:/00AAA/CSV_data/qlib/qlib_data/cn_data --region cn
## 更新wind导出index数据 20210330
处理来自商用软件导出来数据
(1)# normalize
python collector.py normalize_data --source_dir D:/00AAA/CSV_data/index_process --normalize_dir D:/00AAA/CSV_data/qlib/index_process_nor --region CN --interval 1d --symbol_field_name code

(2)##
python scripts/dump_bin.py dump_update --csv_path D:/00AAA/CSV_data/qlib/index_process_nor --qlib_dir D:/00AAA/CSV_data/qlib/cn_1d_sh_nor_dump --symbol_field_name code --date_field_name date --include_fields close, open, high, low, PreviousClosingPrice,IncreaseDecrease, IncreaseDecreaseRate, volume, amount,change,factor

python scripts/dump_bin.py dump_update --csv_path D:/00AAA/CSV_data/qlib/index_process_nor --qlib_dir D:/00AAA/CSV_data/qlib/cn_1d_sh_nor_dump --symbol_field_name code --date_field_name date --exclude_fields date,code

(2)# dump data


python scripts/dump_bin.py dump_all --csv_path D:/00AAA/CSV_data/sh_data_bao_nor --qlib_dir ~/.qlib/qlib_data/sh_data_bao --freq day --symbol_field_name code --date_field_name date --include_fields open,high,low,close,volume,amount,turn,change,factor


## 使用Yahoo collector.py处理导出数据20210326
python collector.py normalize_data --source_dir D:/00AAA/CSV_data/cn_data_csv_2 --normalize_dir D:/00AAA/CSV_data/qlib/cn_1d_sh_nor --region CN --interval 1d --symbol_field_name code


(2)# dump data
python scripts/dump_bin.py dump_all --csv_path D:/00AAA/CSV_data/qlib/cn_1d_sh_nor --qlib_dir D:/00AAA/CSV_data/qlib/cn_1d_sh_nor_dump --freq day --symbol_field_name code --date_field_name date  --exclude_fields date,code


## fund 20210325
python collector.py normalize_data --source_dir D:/00AAA/CSV_data/qlib/cn_fund --normalize_dir D:/00AAA/CSV_data/qlib/cn_fund_nor --region CN --interval 1d --date_field_name FSRQ


python scripts/dump_bin.py dump_all --csv_path D:/00AAA/CSV_data/qlib/cn_fund_nor --qlib_dir D:/00AAA/CSV_data/qlib/cn_fund_nor_dump --freq day --date_field_name FSRQ --include_fields DWJZ,LJJZ





## fund 20210321
# download from eastmoney.com
python collector.py download_data --source_dir ~/.qlib/fund_data/source/cn_1d --region CN --start 2008-11-01 --end 2021-03-21 --delay 0.1 --interval 1d

# normalize
python collector.py normalize_data --source_dir ~/.qlib/fund_data/source/cn_1d --normalize_dir ~/.qlib/fund_data/source/cn_1d_nor --region CN --interval 1d --date_field_name FSRQ

# dump data
cd qlib/scripts
python dump_bin.py dump_all --csv_path ~/.qlib/fund_data/source/cn_1d_nor --qlib_dir ~/.qlib/qlib_data/cn_fund_data --freq day --date_field_name FSRQ --include_fields DWJZ,LJJZ



python scripts/dump_bin.py dump_all COMMAND | VALUE | --csv_path=CSV_PATH --qlib_dir=QLIB_DIR <flags>

python scripts/get_data.py qlib_data --target_dir ~/.qlib/qlib_data/cn_data --region cn



# download from yahoo finance
python collector.py download_data --source_dir D:/00AAA/CSV_data/sh_data --region CN --start 1990-01-01 --end 2021-03-16 --delay 0.1 --interval 1d

# normalize
python collector.py normalize_data --source_dir D:/00AAA/CSV_data/sh_data -normalize_dir D:/00AAA/CSV_data/sh_data_nor --region CN --interval 1d --symbol_field_name symbol

# dump data
python scripts/dump_bin.py dump_all --csv_path D:/00AAA/CSV_data/sh_data_nor --qlib_dir ~/.qlib/qlib_data/sh_data --freq day --exclude_fields date,adjclose,dividends,splits,symbol



# normalize
python collector.py normalize_data --source_dir ~/.qlib/stock_data/source/cn_1d --normalize_dir ~/.qlib/stock_data/source/cn_1d_nor --region CN --interval 1d --symbol_field_name symbol

# dump data
python scripts/dump_bin.py dump_all --csv_path ~/.qlib/stock_data/source/cn_1d_nor --qlib_dir ~/.qlib/qlib_data/qlib_cn_1d --freq 1min --exclude_fields date,adjclose,dividends,splits,symbol


python scripts/dump_bin.py dump_all --csv_path ~/.qlib/stock_data/source/cn_1d_nor --qlib_dir ~/.qlib/qlib_data/qlib_cn_1d --freq day --exclude_fields date,adjclose,dividends,splits,symbol
cd qlib/scripts
python scripts/dump_bin.py dump_all --csv_path ~/.qlib/stock_data/source/cn_1d_nor --qlib_dir ~/.qlib/qlib_data/qlib_cn_1d --freq 1min --exclude_fields date,adjclose,dividends,splits,symbol


python scripts/dump_bin.py dump_update --csv_path ~/.qlib/stock_data/source/cn_1d_nor --qlib_dir ~/.qlib/qlib_data/cn_data --freq 1min --exclude_fields date,adjclose,dividends,splits,symbol

处理来自baostock数据

(1)# normalize
python collector.py normalize_data --source_dir D:/00AAA/CSV_data/sh_data1 --normalize_dir ~/.qlib/stock_data/source/cn_1d_nor2 --region CN --interval 1d --symbol_field_name code
python collector.py normalize_data --source_dir D:/00AAA/CSV_data/sh_data_bao --normalize_dir D:/00AAA/CSV_data/sh_data_bao_nor --region CN --interval 1d --symbol_field_name code

##python scripts/dump_bin.py dump_all --csv_path D:/00AAA/CSV_data/sh_data1 --qlib_dir ~/.qlib/qlib_data/sh_data --symbol_field_name code --date_field_name date --include_fields open,high,low,close,volume,amount,turn,change,factor

(2)# dump data
python scripts/dump_bin.py dump_all --csv_path D:/00AAA/CSV_data/sh_data_bao_nor --qlib_dir ~/.qlib/qlib_data/sh_data_bao --freq day --symbol_field_name code --date_field_name date --include_fields open,high,low,close,volume,amount,turn,change,factor


python scripts/dump_bin.py dump_all --csv_path ~/.qlib/stock_data/source/cn_1d_nor2 --qlib_dir ~/.qlib/qlib_data/qlib_cn_1d2  --symbol_field_name code --date_field_name date --include_fields open,high,low,close,volume,amount,turn,change,factor


python scripts/dump_bin.py dump_all --csv_path ~/.qlib/stock_data/source/cn_1d_nor2 --qlib_dir ~/.qlib/qlib_data/qlib_cn_1d2  --symbol_field_name code --date_field_name date --include_fields open,high,low,close,volume,amount,turn,change,factor


处理来自商用软件导出来数据

(1)# normalize
python collector.py normalize_data --source_dir D:/00AAA/CSV_data/sh_data1 --normalize_dir ~/.qlib/stock_data/source/cn_1d_nor2 --region CN --interval 1d --symbol_field_name code

python collector.py normalize_data --source_dir D:/00AAA/CSV_data/sh_data_bao --normalize_dir D:/00AAA/CSV_data/sh_data_bao_nor --region CN --interval 1d --symbol_field_name code

##python scripts/dump_bin.py dump_all --csv_path D:/00AAA/CSV_data/sh_data1 --qlib_dir ~/.qlib/qlib_data/sh_data --symbol_field_name code --date_field_name date --include_fields open,high,low,close,volume,amount,turn,change,factor

(2)# dump data
python scripts/dump_bin.py dump_all --csv_path D:/00AAA/CSV_data/sh_data_bao_nor --qlib_dir ~/.qlib/qlib_data/sh_data_bao --freq day --symbol_field_name code --date_field_name date --include_fields open,high,low,close,volume,amount,turn,change,factor


python scripts/dump_bin.py dump_all --csv_path ~/.qlib/stock_data/source/cn_1d_nor2 --qlib_dir ~/.qlib/qlib_data/qlib_cn_1d2  --symbol_field_name code --date_field_name date --include_fields open,high,low,close,volume,amount,turn,change,factor


python scripts/dump_bin.py dump_all --csv_path ~/.qlib/stock_data/source/cn_1d_nor2 --qlib_dir ~/.qlib/qlib_data/qlib_cn_1d2  --symbol_field_name code --date_field_name date --include_fields open,high,low,close,volume,amount,turn,change,factor
