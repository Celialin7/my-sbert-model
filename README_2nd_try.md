# SBERT模型第二次拆分传输 - 说明文档

## 🎯 目标
重新拆分和传输正确的SBERT模型文件，确保公司内网能正确加载

## 📊 黄金标准指纹
**文件**: pytorch_model.bin  
**SHA256**: `16cc9e54df6e083272378abec2d75dc34d7a48b5276db3ccc050d18de672ac59`  
**大小**: 470,693,617 bytes (约470MB)  
**来源**: /Users/CeliaLin_1/Desktop/paraphrase-multilingual-MiniLM-L12-v2/pytorch_model.bin

## 🔧 拆分方案

### 方案1: 直接分块文件 (推荐)
- **分块大小**: 45MB
- **分块数量**: 10个
- **文件列表**:
  - model_part_aa (47,185,920 bytes)
  - model_part_ab (47,185,920 bytes)
  - model_part_ac (47,185,920 bytes)
  - model_part_ad (47,185,920 bytes)
  - model_part_ae (47,185,920 bytes)
  - model_part_af (47,185,920 bytes)
  - model_part_ag (47,185,920 bytes)
  - model_part_ah (47,185,920 bytes)
  - model_part_ai (47,185,920 bytes)
  - model_part_aj (46,020,337 bytes)

### 方案2: ZIP压缩后分块
- **ZIP文件**: model_parts.zip (411MB)
- **ZIP分块大小**: 90MB
- **ZIP分块数量**: 5个
- **文件列表**:
  - model_parts_zip_aa (94,371,840 bytes)
  - model_parts_zip_ab (94,371,840 bytes)
  - model_parts_zip_ac (94,371,840 bytes)
  - model_parts_zip_ad (94,371,840 bytes)
  - model_parts_zip_ae (53,933,088 bytes)

## 📤 上传建议

### 推荐方案: 直接上传分块文件
1. 上传 `model_part_aa` 到 `model_part_aj` (10个文件)
2. 每个文件约45MB，符合GitHub 100MB限制
3. 传输过程中损坏概率较低

### 备选方案: 上传ZIP分块
1. 上传 `model_parts_zip_aa` 到 `model_parts_zip_ae` (5个文件)
2. 每个文件约90MB，符合GitHub 100MB限制
3. 需要先解压ZIP，再合并分块

## 🔍 验证步骤

### 在公司内网下载后:
1. 下载所有分块文件
2. 合并文件: `cat model_part_aa model_part_ab ... model_part_aj > pytorch_model.bin`
3. 验证SHA256: `shasum -a 256 pytorch_model.bin`
4. 应该得到: `16cc9e54df6e083272378abec2d75dc34d7a48b5276db3ccc050d18de672ac59`

### 如果使用ZIP方案:
1. 下载所有ZIP分块文件
2. 合并ZIP: `cat model_parts_zip_aa model_parts_zip_ab ... model_parts_zip_ae > model_parts.zip`
3. 解压ZIP: `unzip model_parts.zip`
4. 合并模型分块: `cat model_part_aa model_part_ab ... model_part_aj > pytorch_model.bin`
5. 验证SHA256

## ⚠️ 注意事项
- 确保按字母顺序合并文件
- 验证合并后的文件大小应为 470,693,617 bytes
- 如果SHA256不匹配，说明传输过程中有损坏
- 建议使用方案1 (直接分块)，传输更可靠

## 📝 测试验证
使用测试脚本验证模型是否正确加载:
```python
from sentence_transformers import SentenceTransformer
model = SentenceTransformer("path/to/model/directory")
# 测试句子相似度计算
```

---
**创建时间**: 2024-08-28  
**创建者**: AI Assistant  
**状态**: 准备上传
