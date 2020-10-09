## useMemo: function truyền vào useMemo bắt buộc phải ở trong quá trình render
## useCallback: đó lại là function callback của 1 event nào đó như là onClick chẳng hạn
## Sự khác nhau giữa useEffect và useLayoutEffect
  Tất cả nằm ở thời gian
  useEffect chạy bất đồng bộ và sau một render được hiện lên màn hình
  Trình tự sẽ là:
  Bạn gây ra một event render (thay đổi state, hoặc re-renders từ cha)
  React render Component của bạn (Gọi nó)
  Màn hình được cập nhật UI
  Cuối cùng useEffect chạy
  useLayoutEffect, sẽ chạy khác thứ tự, nó chạy đồng bộ sau một render và trước khi màn hình được cập nhật UI. Trình tự là:
  Bạn gây ra một event render
  React render Component của bạn
  useLayoutEffect chạy, và React đợi đến khi nào nó finish.
  Màn hình được cập nhật UI
  Phần lớn trường hợp, useEffect là lựa chọn đúng. Nếu code của bạn xảy ra trường hợp giật, thay sang useLayoutEffect sẽ giúp bạn giải quyết vấn đề này
