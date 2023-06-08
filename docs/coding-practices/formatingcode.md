---
sidebar_position: 3
---

## Định dạng theo chiều dọc

- Code của bạn không nên quá dày đặc theo chiều dọc, khai báo biến có thể viết liền lại với nhau và không nên có comment hoặc ngăn cách chúng bằng 1 dòng trống, điều đó phá vỡ sự liên kết..
````php
//bad
<?php
 
public class ReporterConfig {
    /**
    * The class name of the reporter listener
    */
    private String m_className;
    /**
    * The properties of the reporter listener
    */
    private List<Property> m_properties = new ArrayList<Property>();
    public void addProperty(Property property) {
    m_properties.add(property);
}

//good
<?php
 
public class ReporterConfig {
    private String m_className;
    private List<Property> m_properties = new ArrayList<Property>();

    public void addProperty(Property property) {
        m_properties.add(property);
    }
}
````

# Khoảng cách giữa các phần
- Gần như tất cả code của bạn được đọc từ trái qua phải, từ trên xuống dưới. Mỗi dòng đại diện cho một biểu thức hoặc một mệnh đề, và mỗi nhóm dòng đại diện cho một mạch logic hoàn chỉnh. Mỗi dòng trống là một dấu hiệu để người đọc xác định một khái niệm mới và riêng biệt
````php
<?php
//good
const [visible, setVisible] = React.useState(false);

const [index, setIndex] = React.useState(0);
````

# Khai báo biến
- Các biến được khai báo càng gần với nơi sử dụng chúng càng tốt. Bởi hàm sử dụng chúng rất ngắn, các biến cục bộ phải đước khai báo ở những dòng đầu tiên của mỗi hàm.
````php
<?php
const getProperties = (item: ItemProps) => {
  if (item.prices != null && item.prices.properties.length > 0) {
    let property = ""
    item.prices.properties.forEach((it: ItemPropertyProps) => {
      property = `${property}${it.name}, `
    })
    return property.substring(0, property.length - 2)
  }
  return null
}
````

# Các hàm phụ thuộc nhau.
- Nếu có một hàm gọi một hàm khác, chúng nên đặt gần nhau. Nếu có thể, hàm gọi nên ở trên hàm được goi, tạo một dòng chảy mã nguồn từ mức cao đến mức thấp. Cũng đừng thu nhỏ font chữ để tăng số lượng ký tự trên 1 dòng màn hình.
````php
<?php
ngOnInit() {
    this.loadData();
}

loadData() {
    this.loadLanguage();

    this.currentMemberId = await this.storage.get('currentMemberId');
}

loadLanguage() {
   // Load language here
}
````

## Định dạng theo chiều ngang
# Việc lùi đầu dòng
- Một file code nên giống một hệ thống hoàn chỉnh hơn là một bản phác thảo sơ sài. Sẽ có thông tin về toàn bộ file, thông tin về các class riêng lẻ trong file, thông tin về các khối lệnh của hàm và các khối lệnh con trong hàm. Mỗi cấp độ của hệ thống này tạo ra một phạm vi mà ở đó bạn có thể khai báo các biến, trong đó các khai báo và câu lệnh được thể hiện một cách rõ ràng.
````php
//bad
<?php
public class FitNesseServer implements SocketServer { private FitNesseContext context; public FitNesseServer(FitNesseContext context) { this.context = context; } public void serve(Socket s) { serve(s, 10000); } public void serve(Socket s, long requestTimeout) { try { FitNesseExpediter sender = new FitNesseExpediter(s, context); sender.setRequestParsingTimeLimit(requestTimeout); sender.start(); } catch(Exception e) { e.printStackTrace(); } } }

//good
<?php
public class FitNesseServer implements SocketServer {
    private FitNesseContext context;

    public FitNesseServer(FitNesseContext context) {
        this.context = context;
    }

    public void serve(Socket s) {
        serve(s, 10000);
    }

    public void serve(Socket s, long requestTimeout) {
        try {
            FitNesseExpediter sender = new FitNesseExpediter(s, context);
            sender.setRequestParsingTimeLimit(requestTimeout); sender.start();
        }
        catch (Exception e) {
            e.printStackTrace();
        }
    } 
}
````