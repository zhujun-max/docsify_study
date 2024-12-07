```js
// 引入必要的模块和插件
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin'); // 生成HTML文件的插件
const { CleanWebpackPlugin } = require('clean-webpack-plugin'); // 清理dist文件夹的插件
const MiniCssExtractPlugin = require('mini-css-extract-plugin'); // 提取CSS到单独文件的插件
const CssMinimizerPlugin = require('css-minimizer-webpack-plugin'); // CSS代码压缩插件
const TerserPlugin = require('terser-webpack-plugin'); // JavaScript代码压缩插件
const webpack = require('webpack'); // Webpack核心库
const ModuleFederationPlugin = require('webpack').container.ModuleFederationPlugin; // Webpack模块联邦插件

module.exports = {
  // 入口文件，Webpack从这里开始构建依赖图
  entry: './src/index.js',

  // 出口配置，指定打包后文件的输出位置、文件名等
  output: {
    filename: '[name].[contenthash].js', // 使用内容哈希生成唯一的文件名
    path: path.resolve(__dirname, 'dist'), // 输出到dist文件夹
    clean: true, // 在每次构建前清理dist文件夹
    publicPath: '/', // 指定资源文件的公共路径
  },

  // 模块配置，定义如何处理不同类型的文件
  module: {
    rules: [
      {
        test: /\.js$/, // 匹配所有.js文件
        exclude: /node_modules/, // 排除node_modules文件夹
        use: {
          loader: 'babel-loader', // 使用Babel加载器
          options: {
            presets: ['@babel/preset-env'], // 使用Babel预设来转换ES6+代码
            cacheDirectory: true, // 启用缓存以提高构建速度
          },
        },
      },
      {
        test: /\.css$/, // 匹配所有.css文件
        use: [
          MiniCssExtractPlugin.loader, // 使用插件的loader来提取CSS到单独文件
          'css-loader', // 使用css-loader来解析CSS文件
        ],
      },
      {
        test: /\.(png|svg|jpg|jpeg|gif)$/i, // 匹配所有图片文件
        type: 'asset/resource', // 将图片作为资源文件处理
      },
      {
        test: /\.(woff|woff2|eot|ttf|otf)$/i, // 匹配所有字体文件
        type: 'asset/resource', // 将字体文件作为资源文件处理
      },
    ],
  },

  // 插件配置，用于执行广泛的任务
  plugins: [
    new HtmlWebpackPlugin({
      template: './src/index.html', // 使用src/index.html作为模板
      filename: 'index.html', // 输出文件名
      minify: {
        // 压缩HTML选项
        collapseWhitespace: true, // 移除空白字符
        removeComments: true, // 移除注释
        minifyJS: true, // 压缩JavaScript（注意：在生产模式下，HtmlWebpackPlugin会自动使用TerserPlugin）
        minifyCSS: true, // 压缩CSS（注意：在生产模式下，MiniCssExtractPlugin会使用CssMinimizerPlugin）
        minifyURLs: true, // 压缩URL
      },
    }),
    new CleanWebpackPlugin(), // 清理dist文件夹
    new MiniCssExtractPlugin({
      filename: '[name].[contenthash].css', // 提取后的CSS文件名
    }),
    // 如果启用了模块联邦，则添加以下插件配置
    new ModuleFederationPlugin({
      name: 'app1', // 应用名称，其他应用通过此名称引用
      filename: 'remoteEntry.js', // 暴露给远程应用的入口文件名
      exposes: {
        './Component': './src/components/Component', // 暴露的模块及其路径
      },
      shared: ['react', 'react-dom'], // 共享的依赖包，其他应用也需要这些包
    }),
  ],

  // 优化配置，用于提高打包性能和运行时性能
  optimization: {
    splitChunks: {
      chunks: 'all', // 将所有代码拆分成单独的块（chunks），包括异步代码
    },
    runtimeChunk: 'single', // 将运行时代码拆分成单独的块，以提高缓存效率
    minimizer: [
      new TerserPlugin({
        terserOptions: {
          compress: {
            drop_console: true, // 移除console语句以减少打包后的文件大小
          },
        },
      }),
      new CssMinimizerPlugin(), // 使用CSS压缩插件来压缩CSS代码
    ],
  },

  // 解析配置，用于指定Webpack如何查找模块
  resolve: {
    extensions: ['.js', '.json', '.css'], // 自动解析这些文件后缀，无需在import/require时指定
  },

  // 模式配置，指定Webpack的运行模式（development或production）
  mode: 'production', // 生产模式，会自动进行代码压缩和优化

  // 开发服务器配置（仅在开发模式下使用）
  devServer: {
    contentBase: path.join(__dirname, 'dist'), // 指定开发服务器静态文件的根目录
    compress: true, // 启用gzip压缩
    port: 9000, // 开发服务器监听的端口
    hot: true, // 启用热模块替换（HMR），允许在运行时更新各种模块而无需完全刷新页面
    historyApiFallback: true, // 支持单页应用（SPA）的路由模式，返回index.html对于所有404请求
    headers: {
      'Access-Control-Allow-Origin': '*', // 允许跨域请求（仅用于开发环境）
    },
  },

  // 实验性特性配置（如模块联邦）
  experiments: {
    outputModule: true, // 启用输出模块的实验性特性，允许Webpack输出ES模块
  },

  // 注意：这个配置文件是一个复杂示例，包含了多个高级功能
  // 实际项目中可能需要根据具体需求进行裁剪和调整
};
```