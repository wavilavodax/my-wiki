# 趋势猎手Pro

趋势追踪策略，40x杠杆，当前0交易等待趋势。

## 策略定位
- 模式：纯趋势追踪，不做均值回归
- 杠杆：40x / 40x
- 方向：双向

## 参数配置
| 参数 | 值 |
|------|-----|
| entry_threshold | 0.08 |
| regime_sensitivity | 0.05 |
| trend_strength_min | 15 |
| exit_on_regime_change | false |
| sl_atr_mult | 2.5 |
| tp_rr_ratio | 4.0 |
| trailing_enabled | false |
| rolling_enabled | true |

## 零交易案例分析

2026-05-06 创建后运行18小时产生0交易，根本原因是市场无趋势（BTC $80,838-$81,693 横盘，波动300+美元，仅±1.05%）。

**证据：** 参数全部放开后仍0交易 → 不是参数问题，是市场无趋势。趋势策略在无趋势市场不交易是正常工作状态。

## 诊断流程：Bot 不交易

1. Bot status = running? → 信号层问题
2. composite signal 触发了 entry_threshold 吗？
   - ADX < trend_strength_min → 信号×0.5
   - regime 非强势 → 再×regime_sensitivity
   - 例：0.15 × 0.5 × 0.5 = 0.037，触发不了0.10阈值
3. 是震荡市吗？趋势策略在震荡市零交易是正常行为
4. 参数全放开后仍0交易 → 市场无趋势，等待或换震荡策略
