<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>配件价格系统</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdn.jsdelivr.net/npm/font-awesome@4.7.0/css/font-awesome.min.css" rel="stylesheet">
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        primary: '#3B82F6',
                        secondary: '#10B981',
                        neutral: '#F3F4F6',
                        dark: '#1F2937'
                    },
                    fontFamily: {
                        sans: ['Inter', 'system-ui', 'sans-serif'],
                    },
                }
            }
        }
    </script>
    <style type="text/tailwindcss">
        @layer utilities {
            .content-auto {
                content-visibility: auto;
            }
            .shadow-custom {
                box-shadow: 0 4px 20px rgba(0, 0, 0, 0.08);
            }
            .transition-custom {
                transition: all 0.3s ease-in-out;
            }
        }
    </style>
</head>
<body class="bg-gray-50 min-h-screen font-sans">
    <div class="container mx-auto px-4 py-8 max-w-3xl">
        

        <main class="bg-white rounded-xl shadow-custom p-6 space-y-6">
            <!-- 物品栏 -->
            <div class="form-group">
                <label class="block text-gray-700 font-medium mb-2" for="itemType">
                    <i class="fa fa-cubes mr-2"></i>物品类型
                </label>
                <div class="relative">
                    <select id="itemType" class="w-full p-3 border border-gray-300 rounded-lg appearance-none bg-white focus:outline-none focus:ring-2 focus:ring-primary/50 focus:border-primary transition-custom">
                        <option value="">请选择物品类型</option>
                        <option value="cpu">CPU</option>
                        <option value="gpu">显卡</option>
                        <option value="memory">内存</option>
                        <option value="hardDrive">硬盘</option>
                        <option value="motherboard">主板</option>
                    </select>
                    <div class="pointer-events-none absolute inset-y-0 right-0 flex items-center px-3 text-gray-700">
                        <i class="fa fa-chevron-down"></i>
                    </div>
                </div>
            </div>

            <!-- 品牌栏 -->
            <div class="form-group">
                <label class="block text-gray-700 font-medium mb-2" for="brand">
                    <i class="fa fa-building-o mr-2"></i>品牌
                </label>
                <div class="relative">
                    <select id="brand" class="w-full p-3 border border-gray-300 rounded-lg appearance-none bg-white focus:outline-none focus:ring-2 focus:ring-primary/50 focus:border-primary transition-custom" disabled>
                        <option value="">请先选择物品类型</option>
                    </select>
                    <div class="pointer-events-none absolute inset-y-0 right-0 flex items-center px-3 text-gray-700">
                        <i class="fa fa-chevron-down"></i>
                    </div>
                </div>
            </div>

            <!-- 型号栏 -->
            <div class="form-group">
                <label class="block text-gray-700 font-medium mb-2" for="model">
                    <i class="fa fa-tag mr-2"></i>型号
                </label>
                <div class="relative">
                    <select id="model" class="w-full p-3 border border-gray-300 rounded-lg appearance-none bg-white focus:outline-none focus:ring-2 focus:ring-primary/50 focus:border-primary transition-custom" disabled>
                        <option value="">请先选择品牌</option>
                    </select>
                    <div class="pointer-events-none absolute inset-y-0 right-0 flex items-center px-3 text-gray-700">
                        <i class="fa fa-chevron-down"></i>
                    </div>
                </div>
            </div>

            <!-- 价格输入 -->
            <div class="form-group">
                <label class="block text-gray-700 font-medium mb-2" for="price">
                    <i class="fa fa-cny mr-2"></i>当日价格
                </label>
                <div class="relative">
                    <input type="text" id="price" placeholder="请输入价格" class="w-full p-3 border border-gray-300 rounded-lg appearance-none bg-white focus:outline-none focus:ring-2 focus:ring-primary/50 focus:border-primary transition-custom" disabled>
                    <div class="pointer-events-none absolute inset-y-0 right-0 flex items-center px-3 text-gray-700">
                        <i class="fa fa-rmb"></i>
                    </div>
                </div>
                <p class="text-sm text-gray-500 mt-1">请输入数字格式的价格</p>
            </div>

            <!-- 按钮区域 -->
            <div class="flex flex-col sm:flex-row gap-4 mt-8">
                <button id="resetBtn" class="flex-1 bg-gray-200 hover:bg-gray-300 text-dark font-medium py-3 px-6 rounded-lg transition-custom flex items-center justify-center">
                    <i class="fa fa-refresh mr-2"></i>重置
                </button>
                <button id="submitBtn" class="flex-1 bg-primary hover:bg-primary/90 text-white font-medium py-3 px-6 rounded-lg transition-custom flex items-center justify-center" disabled>
                    <i class="fa fa-check mr-2"></i>提交
                </button>
            </div>
        </main>

        <!-- 成功提示 -->
        <div id="successModal" class="fixed inset-0 flex items-center justify-center bg-black/50 z-50 hidden">
            <div class="bg-white rounded-lg p-6 max-w-md w-full mx-4 transform transition-all">
                <div class="text-center">
                    <div class="inline-flex items-center justify-center w-16 h-16 rounded-full bg-green-100 text-green-500 mb-4">
                        <i class="fa fa-check text-2xl"></i>
                    </div>
                    <h3 class="text-xl font-bold text-gray-900 mb-2">提交成功</h3>
                    <p class="text-gray-600 mb-6">您的价格信息已成功提交</p>
                    <button id="closeModal" class="bg-primary hover:bg-primary/90 text-white font-medium py-2 px-6 rounded-lg transition-custom">
                        确定
                    </button>
                </div>
            </div>
        </div>
    </div>

    <script>
        // 数据配置
        const itemData = {
            cpu: {
                name: "CPU",
                brands: {
                    intel: {
                        name: "Intel",
                        models: ["酷睿i3-12100F", "酷睿i5-12400F", "酷睿i7-12700K", "酷睿i9-12900K"]
                    },
                    amd: {
                        name: "AMD",
                        models: ["锐龙5 5600X", "锐龙7 5800X", "锐龙9 5900X", "锐龙9 5950X"]
                    }
                }
            },
            gpu: {
                name: "显卡",
                brands: {
                    nvidia: {
                        name: "NVIDIA",
                        models: ["RTX 3060", "RTX 3070", "RTX 3080", "RTX 3090"]
                    },
                    amd: {
                        name: "AMD",
                        models: ["RX 6600 XT", "RX 6700 XT", "RX 6800 XT", "RX 6900 XT"]
                    }
                }
            },
            memory: {
                name: "内存",
                brands: {
                    kingston: {
                        name: "金士顿",
                        models: ["DDR4 8GB 3200MHz", "DDR4 16GB 3200MHz", "DDR4 32GB 3200MHz", "DDR4 64GB 3200MHz"]
                    },
                    corsair: {
                        name: "海盗船",
                        models: ["DDR4 8GB 3600MHz", "DDR4 16GB 3600MHz", "DDR4 32GB 3600MHz", "DDR4 64GB 3600MHz"]
                    }
                }
            },
            hardDrive: {
                name: "硬盘",
                brands: {
                    samsung: {
                        name: "三星",
                        models: ["980 PRO 512GB", "980 PRO 1TB", "980 PRO 2TB", "870 Evo 1TB"]
                    },
                    westernDigital: {
                        name: "西部数据",
                        models: ["SN850 512GB", "SN850 1TB", "SN850 2TB", "Blue 1TB SSD"]
                    }
                }
            },
            motherboard: {
                name: "主板",
                brands: {
                    asus: {
                        name: "华硕",
                        models: ["TUF GAMING B550M-PLUS", "ROG STRIX Z690-A GAMING WIFI", "PRIME H610M-K D4", "TUF GAMING X570-PLUS"]
                    },
                    msi: {
                        name: "微星",
                        models: ["MAG B550M MORTAR WIFI", "MPG Z690I UNIFY", "PRO H610M-G DDR4", "MAG X570 TOMAHAWK"]
                    }
                }
            }
        };

        // DOM元素
        const itemTypeSelect = document.getElementById('itemType');
        const brandSelect = document.getElementById('brand');
        const modelSelect = document.getElementById('model');
        const priceInput = document.getElementById('price');
        const submitBtn = document.getElementById('submitBtn');
        const resetBtn = document.getElementById('resetBtn');
        const successModal = document.getElementById('successModal');
        const closeModalBtn = document.getElementById('closeModal');

        // 更新品牌选择
        itemTypeSelect.addEventListener('change', function() {
            const selectedItem = this.value;
            if (selectedItem) {
                brandSelect.disabled = false;
                updateBrandOptions(selectedItem);
            } else {
                brandSelect.disabled = true;
                brandSelect.innerHTML = '<option value="">请先选择物品类型</option>';
                resetModelAndPrice();
            }
        });

        // 更新型号选择
        brandSelect.addEventListener('change', function() {
            const selectedItem = itemTypeSelect.value;
            const selectedBrand = this.value;
            if (selectedItem && selectedBrand) {
                modelSelect.disabled = false;
                updateModelOptions(selectedItem, selectedBrand);
            } else {
                modelSelect.disabled = true;
                modelSelect.innerHTML = '<option value="">请先选择品牌</option>';
                resetPrice();
            }
        });

        // 更新价格输入状态
        modelSelect.addEventListener('change', function() {
            const selectedItem = itemTypeSelect.value;
            const selectedBrand = brandSelect.value;
            const selectedModel = this.value;
            if (selectedItem && selectedBrand && selectedModel) {
                priceInput.disabled = false;
                priceInput.focus();
            } else {
                resetPrice();
            }
        });

        // 价格输入验证
        priceInput.addEventListener('input', function() {
            validateForm();
        });

        // 提交按钮点击事件
        submitBtn.addEventListener('click', function() {
            if (validateForm()) {
                // 模拟提交数据
                const formData = {
                    itemType: itemData[itemTypeSelect.value].name,
                    brand: itemData[itemTypeSelect.value].brands[brandSelect.value].name,
                    model: modelSelect.value,
                    price: parseFloat(priceInput.value)
                };
                
                console.log('提交的数据:', formData);
                
                // 显示成功提示
                successModal.classList.remove('hidden');
            }
        });

        // 重置按钮点击事件
        resetBtn.addEventListener('click', function() {
            resetForm();
        });

        // 关闭成功提示
        closeModalBtn.addEventListener('click', function() {
            successModal.classList.add('hidden');
            resetForm();
        });

        // 更新品牌选项
        function updateBrandOptions(itemType) {
            const brands = itemData[itemType].brands;
            let options = '<option value="">请选择品牌</option>';
            Object.keys(brands).forEach(brandKey => {
                options += `<option value="${brandKey}">${brands[brandKey].name}</option>`;
            });
            brandSelect.innerHTML = options;
            resetModelAndPrice();
        }

        // 更新型号选项
        function updateModelOptions(itemType, brand) {
            const models = itemData[itemType].brands[brand].models;
            let options = '<option value="">请选择型号</option>';
            models.forEach(model => {
                options += `<option value="${model}">${model}</option>`;
            });
            modelSelect.innerHTML = options;
            resetPrice();
        }

        // 重置型号和价格
        function resetModelAndPrice() {
            modelSelect.disabled = true;
            modelSelect.innerHTML = '<option value="">请先选择品牌</option>';
            resetPrice();
        }

        // 重置价格
        function resetPrice() {
            priceInput.disabled = true;
            priceInput.value = '';
            submitBtn.disabled = true;
        }

        // 重置整个表单
        function resetForm() {
            itemTypeSelect.value = '';
            brandSelect.disabled = true;
            brandSelect.innerHTML = '<option value="">请先选择物品类型</option>';
            modelSelect.disabled = true;
            modelSelect.innerHTML = '<option value="">请先选择品牌</option>';
            priceInput.disabled = true;
            priceInput.value = '';
            submitBtn.disabled = true;
            
            // 移除所有表单元素的焦点
            itemTypeSelect.blur();
            brandSelect.blur();
            modelSelect.blur();
            priceInput.blur();
        }

        // 验证表单
        function validateForm() {
            const price = priceInput.value.trim();
            const priceIsValid = /^\d+(\.\d{1,2})?$/.test(price);
            
            if (priceIsValid) {
                priceInput.classList.remove('border-red-500');
                priceInput.classList.add('border-green-500');
                submitBtn.disabled = false;
                return true;
            } else if (price === '') {
                priceInput.classList.remove('border-red-500', 'border-green-500');
                submitBtn.disabled = true;
                return false;
            } else {
                priceInput.classList.remove('border-green-500');
                priceInput.classList.add('border-red-500');
                submitBtn.disabled = true;
                return false;
            }
        }
    </script>
    
</body>
</html>
    
