# React 2018
tổng quan về react js --> app react được cấu thành từ các component và dễ scale up và bảo trì vì ....

2. Component: có 2 loại simple component (stateless component) and class component(stateful component vì sử dụng state). Component dạng function chỉ chứa props, còn dạng class chứa cả state và props.
	A class component must include render(), and the return can only return one parent element.
	Để truyền dữ liệu qua các component chúng ta dùng props và state
		Thực tế dữ liệu khi truyền qua props sẽ ở trong virtual DOM. This data is not in the actual DOM yet, though.
		Props: component không thể thay đổi props, chỉ read only (vì không có hàm setState())
		State: State như bất kỳ dữ liệu nào cần được lưu và  sửa đổi mà không nhất thiết phải được thêm vào cơ sở dữ liệu. Các thay đổi sẽ chỉ tác động trên view mà không ảnh hưởng đến cơ sở dữ liệu.
			- ví dụ: thêm và xóa các mục khỏi giỏ hàng trước khi xác nhận mua hàng của bạn
		State: coi nhu la private props, khong the truyen vao từ react render. Không thể truy xuất từ ngoài class của nó vào. State lưu trữ state trước đó và state hiện tại
	
	In class component, We’ll need the constructor() to use this, and to receive the props of the parent.
	In addition to taking input data (accessed via this.props), a component can maintain internal state data (accessed via this.state). Thanks to the setState() call, When a component’s state data changes, the rendered markup will be updated by re-invoking render() by .
	Component dạng function chỉ chứa props, còn dạng class chứa cả state và props. Tuỳ theo bài toán cụ thể mình sẽ chọn component cho phù hợp :)

3. Web APIs: 
	Web APIs, which allow a web server to interact with third-party software. 
In this case, the web server is using HTTP requests to communicate to a publicly available URL endpoint containing JSON data.

immutable: không thay đổi, ví như biến const. khi ta render 1 react element thì ta không thể sửa các element bên trong được, sẽ phải định ngĩa và render lại

4. Component Life Cycles:
	componentDidMount (componentDidInsert): được gọi khi component được khởi tạo và vừa hiện lên giao diện
		
# React 2020
## Reconciliation
-- Diff Algorithm === Reconciliation
-- Thông thường Reconciliation dựa vào "index" trong mảng children trong dom tree javascript object để so sánh --> có thể set phụ thuộc sang "key" -- Có liên quan đến shouldComponentUpdate() và PureComponent
-- Khi thay dổi state ở component cha, react gọi hàm render() tại cả cha và con
## Race condition
1. race condition xảy ra khi hai hay nhiều thred cùng đọc, ghi or chia sẻ một vùng dữ liệu 
--> kết quả thực thi mukti thread sẽ phụ thuộc vào thứ tự thực thu thread. Nếu sử dụng cách chờ thread 1 chạy xong rồi chạy thread 2 
--> Nếu thread 1 mãi không chạy xong thì sẽ xảy ra deadlock 
--> Cách giải quyết là tạo 1 vùng dữ liệu chia sẻ cho các thread, các thread chạy vào thực thi và sẽ update vùng dữ liệu đó realtime
## Init React app with antd
1. Create app by CRA: yarn create react-app antd-demo OR npx create-react-app antd-demo
2. Add antd: yarn add antd
3. Add lint: 
    - yarn add -D eslint-config-prettier eslint-plugin-prettier husky lint-staged prettier
    - add file .prettierignore, .prettierrc.json, .eslintignore, .eslintrc.json
3. Add craco: yarn add @craco/craco, yarn add craco-less
4. Create craco.config.js
5. Install storybook: npx -p @storybook/cli sb init
6. Add preset antd for overwriting load config: yarn add -D @storybook/preset-ant-design
7. Change main.js in .storybook: 
      `
      module.exports = {
        stories: ['../src/**/*.stories.mdx', '../src/**/*.stories.@(js|jsx|ts|tsx)'],
        addons: [
          '@storybook/addon-links',
          '@storybook/addon-essentials',
          {
            name: '@storybook/preset-create-react-app',
            options: {
              craOverrides: {
                fileLoaderExcludes: ['less'],
              },
            },
          },
          {
            name: '@storybook/preset-ant-design',
            options: {
              lessOptions: {
                modifyVars: {
                  'primary-color': '#1DA57A',
                  'border-radius-base': '2px',
                },
              },
            },
          },
        ],
      };
      `
8. Add less to storybook by import to preview.js: import 'antd/dist/antd.less'
