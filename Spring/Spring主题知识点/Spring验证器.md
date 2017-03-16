`SpringMVC`服务器验证一种是有两种方式,一种是基于`Validator`接口,一种是使用`Annotaion JSR-303`标准的验证



####基于Validator接口

创建校验类，让其实现Validator接口，覆盖其中两个方法：

* `boolean supports(Class<?> clazz)`

* `void validate(Object obj, Errors errors)`

注册校验器，实现校验：

		@Autowired
    	private Validator indexValidator;

		@InitBinder("homeForm")
    	public void initBinder(WebDataBinder binder) {
        	binder.setValidator(indexValidator);
    	}

在Spring容器中注册验证器：

		<bean id="indexValidator" class="personal.validator.IndexValidator"/>

在控制器中使用验证器：

	@RequestMapping(method = RequestMethod.POST)
    public String submit(Model model, @ModelAttribute("homeForm") @Validated Home homeForm, BindingResult binding) {
        model.addAttribute("homeForm",homeForm);
        String returnVal = "index";
        if (binding.hasErrors()) {
            returnVal = "index_update";
        } else {
            model.addAttribute("homeSess",homeForm);
            model.addAttribute("statusSess","undefault");
        }
        return returnVal;
    }


