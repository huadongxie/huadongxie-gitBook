```
<td class="td_item" align="right">
                建党组织状态：
            </td>
            <td class="td_item_text">
                <input id="PartyOrganizationStatus" class="easyui-combobox" name="PartyOrganizationStatus" panelheight="120" editable="false"
                       data-options="valueField:'SocialUnitPartyCategoryId', groupField:'group', textField:'Text',url:'/basedata/SocialUnitPartyCategory/ListComboSocialUnitPartyCategory'" />
            </td>
```

获取数据是由url:'/basedata/SocialUnitPartyCategory/ListComboSocialUnitPartyCategory' 实现的。

ListComboSocialUnitPartyCategory如下：

```
 public ActionResult ListComboSocialUnitPartyCategory()
        {
            QueryParameter param = new QueryParameter() { TableName = "[basedata].[SocialUnitPartyCategory]" };
            var list = this._socialUnitPartyCategoryService.GetObjects<SocialUnitPartyCategory>(param);
            var categories = SocialUnitPartyCategory.ToEasyTree(list);

            IList result = new ArrayList();

            foreach (var category in categories)
            {
                if (category.children.Count == 0)
                    result.Add(new
                    {

                        SocialUnitPartyCategoryId = category.SocialUnitPartyCategoryId,
                        Text = string.Format("{0} {1}", category.Number, category.Text)
                    });
                else
                {
                    foreach (var child in category.children)
                    {
                        result.Add(new
                        {
                            SocialUnitPartyCategoryId = child.SocialUnitPartyCategoryId,
                            group = string.Format("{0} {1}", category.Number, category.Text),
                            Text = string.Format("{0} {1}", child.Number, child.Text)
                        });
                    }
                }
            }
                        return this.Json(result, JsonRequestBehavior.AllowGet);
        }
```



