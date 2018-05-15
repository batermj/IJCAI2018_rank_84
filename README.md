# IJCAI2018_rank_84
A LI mama IJCAI2018 competion rank 84/5204

特征说明：
我的方案：
1、缺失值填充：
如果缺少的条目很少，就用随机数填充，或者删掉。测试集的话就必须随机填充了。填充方法是，从未缺失的样本中采样，这样填充的话还能符合原来的样本。
如果缺失一定数目，那么就看情况是否能将其单独作为一类，例如本例中的性别缺失，可以理解为，不填性别的，可能用的也很少，转换率也很低，甚至是爬虫玩家。

2、最好将测试数据和训练数据拼起来预测。不过需要注意的是，涉及到统计数据时，要看是否要训练测试一起统计？

3、记得用lbl = preprocessing.LabelEncoder()对id类或者category类进行编码。

4、排序特征。其实也就是cumcount()。尤其是user-item的cum特征，反应了很多问题。

5、统计3天前、2天前、1天前该user对该item的点击次数

6、统计user看过的所有物品中，价格、收藏、销量的排序

7、将pre-category-list当成一次查询，只要输入的关键字相同，这个值也会相同。那么可以将其关键字下的物品的价格、销量、收藏进行排序。同时还要统计最大值。因为只有一个物品和很多个物品时，排第一的意义不同。

8、如果需要分时间，将数据集按天划分到一个字典里面。

9、可以尝试统计点击量中，col1和col2共同实现的次数占col2的比例。这反映了用户的偏好程度。例如当用户性别是女，品牌是香奈儿时，这个比例会高一点。性别是男时，显然要低不少。我在本比赛中，统计的是用户特征和商品特征之间的交互。分母是用户特征。

10、另外，我还统计了原始category特征的转换率替代category特征。毕竟在树结构中，category特征不能直接放进去。

11、数目统计 例如item-id，user-id，shop-id这种。



我的复赛方案：
由于转换率差异巨大，只用7号当天作为训练集和验证集。0-6号用来提取特征。
和初赛类似的特征不再叙述

统计前7天的点击量和交易量

统计十分钟前、十分钟后，该user浏览过该商品、该店铺、该广告几次。但其实在本题中，有大量用户都是只点击了一次，因此这个特征虽然好，但对这种类型的用户并不起作用。

Shop_item_unique：统计了shop里有多少商品。

'brand_cvr','shop_cvr','item_cvr','user_gender_cvr'分别是以7号为主，用hour进行滑窗的转换率

统计一个占比。

总结就是：我们的方案太过依赖于用户的历史记录。对于一些新用户，实用性太差了。参考植物的方案，能更好区分出来。
