Flight Booking System
This I have written as part of my LLD Practice. Please let me know further imporvements that can be done.

Other Design Problems

Functional Requrements-

User should be able to login/signup
Admin can add/delete/update flight details
User Should be able to search flight based on date and destination
User should be able to book/cancel flights
User should get confirmation on booking
=======================================================

✅ FR 1: User Registration

class User{
	String id;
	String name;
	String email;
	String phoneNo;

	//constructor, getter, setters
}

public interface IUserService{
	void registerUser(String name, String email);
	User getUser(String userID);
}

public UserService implements IUserService{
	Map<String,User> users=new HashMap<>(); // ID,USER

	@Override
	public void registerUser(String name, String email){
		String id=randomUID;
		users.put(it,new User(name,email));
	}

	@Override
	User getUser(String userID){
		return users.get(userID);
	}
}
=======================================================

✅ FR 2: Flight Creation (Admin)

public class Flight{
	String id;
	String flightName;
	String from;
	String dst;
	Date date;

	Flight(String flightName, String from, String dst, Date date){

	}
}

public interface IFlightService{
	void addFlight(Flight flight);
	void removeFlight(Flight flight);
	void updateFlight(Flight flight);
	List<Flight> getAllFlights(); 
}

public FlightService implements IFlightService{
	Map<String,Flight> flights=new HashMap<>(); // ID,flight

	@Override
	public void addFLight(Flight flight){
		flights.put(flight.getID(),flight);
	}

	@Override
	public void removeFLight(Flight flight){
		flights.remove(flight.getID());
	}

	@Override
	public void updateFlight(Flight flight){
		flights.put(flight.getID(),flight);
	}

	@Override
	List<Flight> getAllFlights(){

	}
}
=======================================================

✅** FR 3: Search Flights**

public class SearchCriteria{
	String source;
	String dst;
	String date;
}

public interface IFlightSearchService{
	List<Flight> searchFlights(SearchCriteria criteria);
}

public class FlightSearchService implements IFlightSearchService{
	IFlightService flightservice;

	FlightSearchService(IFlightService flightservice){
		flightservice=flightservice;
	}

	@Override
	List<Flight> searchFlights(SearchCriteria criteria){
		return flightservice.getAllFlights() ==>Add more filters based on criteria //
	}
}
=======================================================

✅ FR 4: Book/Cancel a Flight

class Booking{
	String bookingID;
	String from;
	String to;
	Date date;
	String userId;
	String flightID;	
}

public interface IBookingService{
	Booking bookFlight(String userID, String bookingiD);
	void cancelBooking(String bookingID);
}

public class BookingService implements IBookingService{
	Map<String,Booking> bookings=new HashMap<>();

	@Override
	Booking bookFlight(String userID, String flightID){
		//add mapping in map
	}

	@Override
	void cancelBooking(String bookingiD){
		//delete from map
	}
}
=======================================================

✅ FR 5: Make Payment (Strategy + Factory)

public interface PaymentStartegy{
	void pay(double amount);
}

public class CreditCardPayment implements PaymentStartegy{
	@Override
	void pay(double amount){

	}
}

public class UPIPayment implements PaymentStartegy{
	@Override
	void pay(double amount){
		
	}
}

public class PaymentFactory{
	public static PaymentMethod getPaymentMethod(String type){
		if(type==CREDIT) return new CreditCardPayment();
		else if(type==UPI) return new UPIPayment();
		else Exception THrow();
	}
}


public class PaymentService{
	public Payment processPayment(String bookingID, PaymentMethod method){
		method.pay();
		return new Payment();
	}
}
=======================================================

✅ FR 6: Notifications

public interface INotificationSerice{
	void sendNotification(String userID, String msg);
}

public class NotificationSerice implements INotificationSerice{
	
	@Override
	void sendNotification(String userID, String msg){

	}
}
=======================================================

✅ FINAL BOSS: FlightBookingFacade

public class FlightBookingService{
	IUserService userService=new UserService(); // ==> For User login
	IFlightService flightService=new FlightService(); // ==> For admin
	IFlightSearchService flightSearchService=new FlightSearchService(); =>> For Searching
	IBookingService bookingService=new BookingService(); // ==> for booking
	IPaymentService paymenetService=new IPaymentService(); // ==> For Payment
	INotificationSerice notificationSerice=new NotificationSerice(); // ==> For notification

	//Register User
	public void registerUser(String name, String email){
		userService.registerUser(name,email);	
	}

	//Admin adding flight
	public void addFlight(Flight flight){
		flightService.addFlight(flight);
	}

	//Search for flight
	public List<Flight> searchFlights(SearchCriteria criteria){
		return flightSearchService.searchFlights(criteria);
	}

	//book flight
	public Booking bookFlight(String userId, String flightID, String paymentType){
		Booking booking=bookingService.bookFlight(userId,flightID);
		PaymentService paymentService=new PaymentService();
		PaymentMethod method=PaymentFactory.getPaymentMethod(type);
		paymentService.processPayment(booking.getID(),method);
		notificationSerice(userID,"Booked Flight");
	}

	public void cancelBooking(String userID, String bookingID){
		bookingService.cancelBooking(bookingID);
		notificationSerice(userID,"Cancelled Flight");
		return;
	}
}
======================= Client Code =======================

FlightBookingService flightBookingService=new FlightBookingService();

flightBookingService.registerUser("mukul","mukul@gmail.com");

Flight flight=new Flight("F101","Delhi","Hyderabad",Date);
flightBookingService.addFlight(flight);

SearchCriteria criteria=new SearchCriteria("Delhi", "Hyderabad", Date);
List<Flight> flights=flightBookingService.searchFlights(criteria);

if(!flights.empty()){
	Booking booking=flightBookingService.bookFlight("User1",flights.get[0].getID(),"UPI");
