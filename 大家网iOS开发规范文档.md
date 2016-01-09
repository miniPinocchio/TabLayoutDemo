大家网iOS开发规范文档

---

1. 命名规范

    此类问题虽然不会影响代码的可运行性,但是会让后续的维护更新工作变得异常困难!尤其换了新人!

整个项目名称的命名

- 如大家论坛最好命名为全英文TopsageForum，djlt次之,其他项目依此类推

项目中的所有类命名

- 加类前缀，统一为该项目名称的首字母缩写，如大家论坛的项目可命名为TFxxxx，分类可按情况起名，如整个项目都用得上则为 UIView+Extension(举例)，只个人用可为UIView+MJExtension(仍建议命名Extension)

项目中模块的命名

- 模块名称应按行业标准命名，如 个人中心 模块命名为 profile，应按开发文档命名，拿不定主意可集体商量决定，统一即可

属性及视图控件的命名

- 不可命名如label1,label2,label3...或让人不明所以的命名，要能见名知意，如用户名显示的标签可以起名usernameLabel，头像可命名iconView等等

方法的命名

- 如 登陆成功刷新界面 可以命名为 changeUIforLogin，要能见名知意

宏命名

- 首字母为大写单词，单词之间用下划线分开:

    	#define SCREEN_WIDTH  ([UIScreen mainScreen].bounds.size.width)  // 屏幕的宽度;
    	#define W_Multiple  (SCREEN_WIDTH/375.0))   // 横向适配倍数,以375 x 667尺寸作基础

总结

- 命名规范普遍为驼峰式命名,争取做到让人一目了然,不能使用汉语拼音甚或瞎起名



2. 注释规范

    对代码所做的工作打注释,可以让后续接手的开发人员容易理解你个人的代码风格,也易于查找/改动来做事情,可是说是 十分有价值的事情!

对类打注释

- 位置为 .h文件上边注释 最后一行 "//" 后,声明此类的性质

对.h文件

- 对头文件声明的属性/方法 打 文档注释
                //
                //  TFUser.h
                //  djlt
                //
                //  Created by macmini04 on 15/12/25.
                //  Copyright © 2015年 com.topsage.djlt. All rights reserved.
                //  用户模型
      
                #import <Foundation/Foundation.h>
      
                @interface TFUser : NSObject
                /** 用户ID */
                @property (nonatomic, copy) NSString *uid;
                /** 头像 */
                @property (nonatomic, copy) NSString *headimg;
                /** 性别 */
                @property (nonatomic, copy) NSString *gender;
                /** 用户昵称 */
                @property (nonatomic, copy) NSString *username;
                /** 用户真实姓名 */
                @property (nonatomic, copy) NSString *realname;
                /** 用户所属群组ID */
                @property (nonatomic, copy) NSString *groupid;
                /** 用户所属群组名称(查看用户返回) */
                @property (nonatomic, copy) NSString *grouptitle;
                /** 用户所属群组名称(登陆返回) */
                @property (nonatomic, copy) NSString *userlevel;
                /** 个性签名 */
                @property (nonatomic, copy) NSString *bio;
                /** 新消息提醒个数 */
                @property (nonatomic, copy) NSString *pmprompt;
                /** 积分 */
                @property (nonatomic, copy) NSString *credits;
                /** 威望 */
                @property (nonatomic, copy) NSString *extcredits1;
                /** 金币 */
                @property (nonatomic, copy) NSString *extcredits2;
                /** 经验 */
                @property (nonatomic, copy) NSString *extcredits3;

对.m文件

- 对.m文件里的类拓展声明的属性/方法/UI控件打注释

                #import "TFLoginHeader.h"
                #import "TFUser.h"
    
                @interface TFLoginHeader ()
                /** 头像 */
                @property (weak, nonatomic) IBOutlet UIImageView *iconView;
                /** 性别 */
                @property (weak, nonatomic) IBOutlet UIImageView *sexView;
                /** 用户名 */
                @property (weak, nonatomic) IBOutlet UILabel *usernameView;
                /** 等级标签 */
                @property (weak, nonatomic) IBOutlet UILabel *levelView;
                /** 个性签名标签 */
                @property (weak, nonatomic) IBOutlet UILabel *signView;
                /** 积分 */
                @property (weak, nonatomic) IBOutlet UILabel *scoreView;
                /** 经验 */
                @property (weak, nonatomic) IBOutlet UILabel *expericeView;
                /** 威望 */
                @property (weak, nonatomic) IBOutlet UILabel *prestigeView;
                /** 金币 */
                @property (weak, nonatomic) IBOutlet UILabel *coinView;
    
                @end

对代码的作用实现打注释

- 同一作用部分只注释一处即可,位置应为此段代码的前面
                /**
                 *  重写push方法,拦截push操作,拦截到所有push进来的控制器
                 *
                 *  @param viewController 即将push进来的控制器
                 */
                - (void)pushViewController:(UIViewController *)viewController animated:(BOOL)animated {
      
                #warning 每一个push进来的控制器都要注册切换背景模式的观察者,这句很危险
                    //每一个push进来的控制器都要注册切换背景模式的观察者
                    //    [[NSNotificationCenter defaultCenter] addObserver:viewController selector:@selector(changeShowStyle) name:ChangeStyle object:nil];
      
                    if (self.viewControllers.count > 0) { //这是push进来的控制器不是第一个控制器(根控制器),需要设置统一的导航栏item,底部tabbar也需要隐藏
                        //自动显示和隐藏tabbar
                        viewController.hidesBottomBarWhenPushed = YES;
      
                        //设置导航栏的内容
                        //左边的返回按钮
                        viewController.navigationItem.leftBarButtonItem = [UIBarButtonItem itemWithTarget:self action:@selector(back) image:@"back" highImage:@"back"];
      
                        //右边的更多按钮(举例)
                        viewController.navigationItem.rightBarButtonItem = [UIBarButtonItem itemWithTarget:self action:@selector(more) image:@"more" highImage:@"more"];
      
                    }
      
                    [super pushViewController:viewController animated:animated];
                }
- 及时换行及加空格，步骤之间可控1~2行,及时删除无效代码，如注释后无用的代码，可保留一些知识点 供同事间学习交流
- 适当使用#pragma mark - XXXX 为相同作用类型的方法划分区域

3.留下最有用的代码,及时删除无效的代码

    一个功能的实现方法有很多种,尽可能运用自己掌握的最高级高效的方式,开发过程中若需要打印验证或临时代码辅助开发,使用完毕须及时删除,或后期重构代码时,须把之前的未封装代码删除,避免混淆视听.只留下有效代码或对自己及同事有借鉴/学习意义的注释及代码并标记清楚

	

4.对代码的封装

    这是对代码业务功能的抽取划分,也是对代码运行性能的优化,不仅检验开发人员的水准,更是对以后的开发工作做铺垫(如写一个工具类,可以拿到以后其他模块或项目中来用,或写一个分类,可以大大提高开发效率!)

- 对代码进行有效的封装,而不是无用的代码转移
- 对频繁调用的代码尽可能的封装优化, 如 - (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath

5.对代码的性能优化

    一个有长远发展的项目,势必代码量会越来越多,功能越来越多,越来越重量级,因此即使对一个微小视图控件的选择都是有必要的，代码的优化性做得好不好,就是影响项目运行流畅度及用户体验的绝对硬指标!这块应该予以重视!

- 如能用一个label来做的事,决不用一个button,因为button里包括了自身View的背景图等属性和imageView和label,更加重量级,而且没必要,纯属浪费;
- 继承自UITableViewController的Controller的self.view=self.tableView,而不要继承自UIViewController拿到空白的View再盖一层tableView,其他如collectionViewController等等依次类推),尽量避免浪费

---

在开发工作中拿不定主意或没有好的思路,应大方说出来,大家一起讨论出主意,也可活跃办公室气氛,提高工作积极性
