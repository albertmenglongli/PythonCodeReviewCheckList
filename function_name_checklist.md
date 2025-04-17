Python函数命名CodeReview检查清单：

    1. 动词准确性
        ✅ 检查函数名是否准确使用动词（如generate_report()优于report()）
        ✅ 及物动词需带宾语语义（parse_config()正确，parse()不完整）
        ✅ 不及物动词需独立表达动作（wait_for_response()）
        ✅ 时态与语态规范，永远使用现在时主动语态：
            serialize_to_json() ✅
            禁止serializing_json() ❌
            禁止json_serialized() ❌

    2. 对偶操作强制配对
        ✅ 互补操作需命名对称：
            open() / close()
            acquire_lock() / release_lock()
            enable_logging() / disable_logging()

    3. 命名一致性规范
        ✅ 相同操作使用相同动词：避免混用retrieve/fetch/get
        ✅ 模块内函数风格统一（如全用下划线或全用驼峰）

    4. 资源消耗级别语义
        ✅ 低开销操作用get_xxx()（如get_user_id()）
        ✅ 高开销操作用fetch/calculate（如fetch_remote_data()）
        ✅ 缓存操作建议cached_get_xxx()

    5. ✅ 函数返回值需与命名语义一致：
        get_xxx()：返回值应为具体对象或数据
        is_xxx()：返回值应为布尔值:
            布尔返回值强制前缀
            ✅ 必须使用is_/has_/can_前缀：
                is_valid() ✅
                has_permission() ✅
                禁止check_valid() ❌
        禁止返回值与函数名语义不符

    6. 副作用明确性原则
        ✅ 修改状态时使用强动作动词：
            mutate_state()
            update_cache()
            禁止handle_data() ❌（副作用不明确）
    
    7. 参数顺序映射命名
        ✅ 函数名需反映参数顺序：
            convert_currency(amount, from_curr, to_curr) ✅
            merge_datasets(primary, secondary) ✅
            禁止使用不明确的参数顺序（如merge_datasets(secondary, primary)）❌
    
    8. 领域专用术语
        ✅ 优先使用业务领域词汇：
            金融场景用reconcile_transactions() ✅
            替代通用process_data() ❌
        ✅ 避免使用容易混淆的缩写或词汇
            优先使用具体描述：user_data、transaction_info ✅
            禁止使用data、info等模糊词汇 ❌

    10. 上下文冗余消除
        ✅ 类方法避免重复类名：
            User.get_profile() ✅
            禁止User.get_user_profile() ❌
    
    11. 拼写校验强制项
        ✅ 使用IDE拼写检查插件验证：
            initialise（英式）vs initialize（美式）需统一

    12. 时间相关函数命名
        ✅ 涉及时间的函数需明确单位或范围：
            get_current_timestamp() ✅ 
            calculate_duration_in_seconds() ✅
            禁止get_time() ❌
