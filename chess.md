Chess
This I have written as part of my LLD Practice. Please let me know further imporvements that can be done

This was asked to me in Microsoft in March 2025, both in 3rd and 4th round, and also to my friend in Salesforce last round same month.

Other Design Problems

Functional Requrements -

8*8 Board
Pieces(Pawn, Rook, Bishop, King, Queen)
Players
Game Logic
Game controller (main service layer)
enum PieceType{
	PAWN, ROOK, BISHOP, KNIGHT, QUEEN, KING
}

enum Color{
	WHITE, BLACK
}
class Player{
	String name;
	Color color;
}

class Cell{
	int x,y;
	Piece piece;

	boolean isEmpty(){

	}

	Piece getPiece(){

	}

	void setPiece(Piece piece){

	}
}
abstract class Piece{
	Position postion;
	Color color;	

	public Piece(){
		//constructor
	}

	abstact boolean isValidMove(Position initial, Position final);
}

class King extends Piece{
	public King(Position postion, Color color){
		super(position,color);
	}

	@Overrirde
	boolean isValidMove(Position initial, Position final){

	}
}

public class PieceFactory{
	static Piece createPiece(PieceType type, Color color, Position position){
		if(type=="KING"){
			return new King(position,color);
		}
		else if(type=="ROOK"){
			return new ROOK(position,color);
		}
		else{
			throwException();
		}
	}
}
class ChessBoard{
	static ChessBoard instance;
	Piece[][] board;

	private ChessBoard(){
		this.board=new Piece[8][8];
		initialiseBoard();
	}


	static ChessBoard getInstance(){
		if(instance==NULL) instance= new ChessBoard();
		return instance;
	}

	void initialiseBoard(){

	}

	Piece getPiece(Position position){

	}

	void displayBoard(){

	}

}
public class Game{
	ChessBoard chessboard;
	Player player1,player2;
	Player currentPlayer;

	Game(Player p1, Player p2){
		chessboard=ChessBoard.getInstance();
		player1=p1;
		player2=p2;
		currentPlayer=player1;
	}

	void play(){
		Scanner sc=new Scanner(System.in);
		while(true){
			board.displayBoard();
			System.out.print("User: "+u1+" Turn");
			System.out.print("Enter Move: "); 

			int startX=sc.nextInt();
			int startY=sc.nextInt();
			int endX=sc.nextInt();
			int endY=sc.nextInt();

			Cell start=new Cell(startX,startY);
			Cell end=new Cell(endX,endY);

			Piece piece=start.getPiece();

			if(piece.isValidMove(board.getBoard(),start,end)){
			
			}
		}
	}

	void switchTurn(){

	}

	boolean isGameOver(){
		//checkmate logic
	}

	void makeMove(Position from, Position to){

	}
}
====================== Client Code ======================

Player p1=new Player("Mukul",Color.WHITE);
Player p2=new Player("Vijay",Color.BLACK);
Game game=new Game(p1,p2);
game.play();
