# ServerDateSwift
func serverTimeReturn  that allows you to  find current date in Swift 4.1

Use this function for find server date in Swift.

func serverTimeReturn(completionHandler:@escaping (_ getResDate: NSDate?) -> Void){
        
        let url = NSURL(string: "http://www.google.com")
        let task = URLSession.shared.dataTask(with: url! as URL) {(data, response, error) in
            let httpResponse = response as? HTTPURLResponse
            if let contentType = httpResponse!.allHeaderFields["Date"] as? String {
                
                let dFormatter = DateFormatter()
                dFormatter.dateFormat = "EEE, dd MMM yyyy HH:mm:ss z"
                let serverTime = dFormatter.date(from: contentType)
                completionHandler((serverTime! as NSDate) )
            }
        }
        
        task.resume()
    }
    
   # func viewDidLoad() 
    override func viewDidLoad() {
        super.viewDidLoad()
      serverTimeReturn { (getResDate) -> Void in
            let dFormatter = DateFormatter()
            dFormatter.dateStyle = DateFormatter.Style.long
            dFormatter.timeStyle = DateFormatter.Style.long
            let timeZone = NSTimeZone(name: "UTC")
            dFormatter.timeZone = timeZone! as TimeZone
           // dFormatter.timeZone = NSTimeZone(abbreviation: "GMT")! as TimeZone
           // let dateGet = dFormatter.string(from: getResDate! as Date)
           var ServerDate = Date() 
           ServerDate = getResDate! as Date
        }
     }
