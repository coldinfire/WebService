## WebService
	WebService是一种跨编程语言和跨操作系统平台的远程调用技术。
	(1) XML+XSD，SOAP，WSDL，UDDI(目录服务，提供WebService服务端的注册和搜索功能)
	(2) WebService的工作调用原理：对客户端而言，我们给这各类WebService客户端API传递wsdl文件的url地址，这些API就会创建出底层的代理类，
		我调用这些代理，就可以访问到webservice服务。代理类把客户端的方法调用变成soap格式的请求数据再通过HTTP协议发出去，并把接收到的soap数据变成返回值返回。
		对服务端而言，各类WebService框架的本质就是一个大大的Servlet，当远程调用客户端给它通过http协议发送过来soap格式的请求数据时，它分析这个数据，
		就知道要调用哪个java类的哪个方法，于是去查找或创建这个对象，并调用其方法，再把方法返回的结果包装成soap格式的数据，通过http响应消息回给客户端。
## SOAP
	(1) SOAP协议 = HTTP协议 + XML数据格式：简单对象访问协议，使用http发送XML格式的数据。
	(2) SOAP协议定义了SOAP消息的格式，SOAP协议是基于HTTP协议的，SOAP也是基于XML和XSD的，XML是SOAP的数据编码方式。
	(3) 协议的格式
		Envelope：必须有，此元素将整个 XML 文档标识为一条SOAP消息
		Header：可选元素，包含头部信息
		Body：必须有，包含所有调用和响应信息
		Fault：可选元素，提供有关在处理此消息时所发生的错误信息
## WSDL
	(1) WebService客户端要调用一个WebService服务，首先要有知道这个服务的地址在哪，以及这个服务里有什么方法可以调用。
		所以，WebService务器端首先要通过一个WSDL文件来说明自己家里有啥服务可以对外调用，服务是什么（服务中有哪些方法
		方法接受的参数是什么，返回值是什么），服务的网络地址用哪个url地址表示，服务通过什么方式来调用。
	(2) WSDL(Web Services Description Language)就是这样一个基于XML的语言，说明服务地址，服务类，方法、参数和返回值。
		它是WebService客户端和服务器端都能理解的标准格式。
	(3)  WSDL文件保存在Web服务器上，通过一个url地址就可以访问到它。
		客户端要调用一个WebService服务之前，要知道该服务的WSDL文件的地址。
	(4) 文档结构
		● <service>    服务视图，webservice的服务结点，它包括了服务端点
		● <binding>     为每个服务端点定义消息格式和协议细节
		● <portType>   服务端点，描述 web service可被执行的操作方法，以及相关的消息，通过binding指向portType
		● <message>   定义一个操作（方法）的数据参数(可有多个参数)
		● <types>        定义 web service 使用的全部数据类型
	(5) 注解方法
		@WebService-定义服务，在public class上边
			targetNamespace：指定命名空间
			name：portType的名称
			portName：port的名称
			serviceName：服务名称
			endpointInterface：SEI接口地址，如果一个服务类实现了多个接口，只需要发布一个接口的方法，
				可通过此注解指定要发布服务的接口。
		@WebMethod-定义方法，在公开方法上边
			operationName：方法名
			exclude：设置为true表示此方法不是webservice方法，反之则表示webservice方法
		@WebResult-定义返回值，在方法返回值前边
			name：返回结果值的名称
		@WebParam-定义参数，在方法参数前边
			name：指定参数的名称
		作用：
			通过注解，可以更加形像的描述Web服务。对自动生成的wsdl文档进行修改，为使用者提供一个更加清晰的wsdl文档。
			当修改了WebService注解之后，会影响客户端生成的代码。调用的方法名和参数名也发生了变化，必须重新生成客户端代码
## WebService开发
	(1) 服务端开发
		把公司内部系统的业务方法发布成WebService服务，供远程合作单位和个人调用。
	(2) 客户端开发
		调用别人发布的WebService服务，如调用天气预报的Webservice服务等。
## WebService发布
	如何发布一个Web服务： 
	(1) 在类上添加@WebService注解 
	（注：此注解是jdk1.6提供的，位于javax.jws.WebService包中） 
	(2) 通过EndPoint(端点服务)发布一个WebService 
	（注：EndPoint是jdk提供的一个专门用于发布服务的类，该类的publish方法接收两个参数，一个是本地的服务地址，二是提供服务的类。位于 javax.xml.ws.Endpoint包中） 
	(3) 注： 
		类上添加注解@WebService，类中所有非静态方法都会被发布； 
		静态方法和final方法不能被发布； 
		方法上加@WebMentod(exclude=true)后，此方法不被发布；
## 适用场合
	(1) 跨防火墙
	(2) 应用程序集成，可以很容易的集成不同结构的应用程序
	(3) B2B集成
	(4) 软件和数据重用
## SoapUI
	SoapUI是一个开源测试工具，通过soap/http来检查、调用、实现Web Service的功能/负载/符合性测试。
	使用soapUI可以非常方便的实现接口的功能测试、稳定性测试、压力测试、性能测试等