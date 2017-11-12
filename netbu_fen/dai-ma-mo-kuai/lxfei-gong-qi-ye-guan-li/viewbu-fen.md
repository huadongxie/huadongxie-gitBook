调用 链接 ~/basedata/Corporation/Index

控制器中实现方法：

```
        public ActionResult Index()
        {
            ViewResult result;

            switch (CurrentUser.SocialUnitType)
            {
                case (int)SocialUnitType.Division:
                    result = this.View("DivisionSocialOrganization");
                    break;

                default:
                    result = this.View("SocialOrganization");
                    break;
            }

            return result;
        }
```



