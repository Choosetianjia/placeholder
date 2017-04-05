# placeholder
用到表单标签时候，placeholder，兼容性问题
<script>
var JPlaceHolder = {
    //检测
    _check: function() {
        return 'placeholder' in document.createElement('input');
    },
    //初始化
    init: function() {
        if (!this._check()) {
            this.fix();
        }
    },
    //修复
    fix: function() {
        jQuery(':input[placeholder]').each(function(index, element) {
            var self = $(this),
                txt = self.attr('placeholder');
            self.wrap($('<div></div>').css({
                position: 'relative',
                zoom: '1',
                border: 'none',
                background: 'none',
                padding: 'none',
                margin: 'none'
            }));
            var pos = self.position(),
                h = self.outerHeight(true),
                paddingleft = self.css('padding-left');
            var holder = $('<span></span>').text(txt).css({
                position: 'absolute',
                left: pos.left,
                top: pos.top + 8,
                height: h,
                lienHeight: h,
                paddingLeft: paddingleft,
                color: '#aaa'
            }).appendTo(self.parent());
            self.focusin(function(e) {
                holder.hide();
            }).focusout(function(e) {
                if (!self.val()) {
                    holder.show();
                }
            });
            holder.click(function(e) {
                holder.hide();
                self.focus();
            });
        });
    }
};
//执行
jQuery(function() {
    JPlaceHolder.init();
});
//验证
$(".ulogin").validate({
    rules: {
        user: "required"
    },
    messages: {
        user: "内容不能为空"
    }
});
</script>
