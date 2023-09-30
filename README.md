# GXJQJ
I am Chiyu yung, 5.3 growing like a tree
$ git clone https://github.com/YOUR-USERNAME/YOUR-REPOSITORY
> Cloning into `Spoon-Knife`...
> remote: Counting objects: 10, done.
> remote: Compressing objects: 100% (8/8), done.
> remove: Total 10 (delta 1), reused 10 (delta 1)
> Unpacking objects: 100% (10/10), done.
> number = random.randint(1, 100)

print("猜猜这个数字是多少？")

for i in range(5):
    guess = int(input("请输入一个数字："))
    if guess == number:
        print("恭喜你，猜对了！")
        break
    elif guess < number:
        print("你猜的数字太小了，再试一次吧。")
    else:
        print("你猜的数字太大了，再试一次吧。")

if guess != number:
    print("很遗憾，你没有猜对。答案是：", number)

    package demo02.clock.chengbao;

import java.util.HashMap;
import java.util.Scanner;

public class Game {
    private Room currentRoom;
    private HashMap<String,Handler> handlers=new HashMap<String,Handler>();

    public Game()
    {
        handlers.put("go", new HandlerGo(this));
        handlers.put("bye", new HandlerBye(this));
        handlers.put("help", new HandlerHelp(this));
        createRooms();
    }
    private void createRooms()
    {
        Room outside, lobby, pub, study, bedroom,bedroom1;
        //    制造房间
        outside = new Room("城堡外");
        lobby = new Room("大堂");
        pub = new Room("小酒吧");
        study = new Room("书房");
        bedroom = new Room("卧室");
        bedroom1 =new Room("次卧");
        //    初始化房间的出口
        outside.setExit("east",lobby);
        outside.setExit("south",study);
        outside.setExit("west",pub);
        lobby.setExit("west", outside);
        pub.setExit("east", outside);
        study.setExit("north",outside);
        study.setExit("east",bedroom);
        bedroom.setExit("west", study);
        bedroom.setExit("up", bedroom1);
        bedroom1.setExit("down", bedroom);

        currentRoom = outside;  //    从城堡门外开始
    }

    private void printWelcome() {
        System.out.println();
        System.out.println("欢迎来到城堡！");
        System.out.println("这是一个超级无聊的游戏。");
        System.out.println("如果需要帮助，请输入 'help' 。");
        System.out.println();
        showPrompt();
    }
    // 以下为用户命令
    public void goRoom(String direction)
    {
        Room nextRoom = currentRoom.getExit(direction);


        if (nextRoom == null) {
            System.out.println("那里没有门！");
        }
        else {
            currentRoom = nextRoom;
            showPrompt();
        }
    }
    public void showPrompt()
    {
        System.out.println("现在你在" + currentRoom);
        System.out.print("出口有：");
        System.out.print(currentRoom.getExitDesc());
        System.out.println();
    }
    public void play()
    {     Scanner in=new Scanner(System.in);
        while ( true ) {
            String line = in.nextLine();
            String[] words = line.split(" ");
            Handler handler =handlers.get(words[0]);
            String value ="";
            if(words.length>1)
                value = words[1];
            if(handler !=null)
            {
                handler.doCmd(value);
                if(handler.isBye())
                {
                    break;
                }
            }
        }
    }
    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        Game game = new Game();
        game.printWelcome();
        game.play();
        System.out.println("感谢您的光临。再见！");
        in.close();
    }

}
复制代码
Handler类

复制代码
package demo02.clock.chengbao;

import java.util.HashMap;
import java.util.Scanner;

public class Game {
    private Room currentRoom;
    private HashMap<String,Handler> handlers=new HashMap<String,Handler>();

    public Game()
    {
        handlers.put("go", new HandlerGo(this));
        handlers.put("bye", new HandlerBye(this));
        handlers.put("help", new HandlerHelp(this));
        createRooms();
    }
    private void createRooms()
    {
        Room outside, lobby, pub, study, bedroom,bedroom1;
        //    制造房间
        outside = new Room("城堡外");
        lobby = new Room("大堂");
        pub = new Room("小酒吧");
        study = new Room("书房");
        bedroom = new Room("卧室");
        bedroom1 =new Room("次卧");
        //    初始化房间的出口
        outside.setExit("east",lobby);
        outside.setExit("south",study);
        outside.setExit("west",pub);
        lobby.setExit("west", outside);
        pub.setExit("east", outside);
        study.setExit("north",outside);
        study.setExit("east",bedroom);
        bedroom.setExit("west", study);
        bedroom.setExit("up", bedroom1);
        bedroom1.setExit("down", bedroom);

        currentRoom = outside;  //    从城堡门外开始
    }

    private void printWelcome() {
        System.out.println();
        System.out.println("欢迎来到城堡！");
        System.out.println("这是一个超级无聊的游戏。");
        System.out.println("如果需要帮助，请输入 'help' 。");
        System.out.println();
        showPrompt();
    }
    // 以下为用户命令
    public void goRoom(String direction)
    {
        Room nextRoom = currentRoom.getExit(direction);


        if (nextRoom == null) {
            System.out.println("那里没有门！");
        }
        else {
            currentRoom = nextRoom;
            showPrompt();
        }
    }
    public void showPrompt()
    {
        System.out.println("现在你在" + currentRoom);
        System.out.print("出口有：");
        System.out.print(currentRoom.getExitDesc());
        System.out.println();
    }
    public void play()
    {     Scanner in=new Scanner(System.in);
        while ( true ) {
            String line = in.nextLine();
            String[] words = line.split(" ");
            Handler handler =handlers.get(words[0]);
            String value ="";
            if(words.length>1)
                value = words[1];
            if(handler !=null)
            {
                handler.doCmd(value);
                if(handler.isBye())
                {
                    break;
                }
            }
        }
    }
    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        Game game = new Game();
        game.printWelcome();
        game.play();
        System.out.println("感谢您的光临。再见！");
        in.close();
    }

}
复制代码
HandlerBye类

复制代码
package demo02.clock.chengbao;

public class HandlerBye extends Handler {

    HandlerBye(Game game) {
        super(game);
        // TODO Auto-generated constructor stub
    }

    @Override
    public boolean isBye() {
        // TODO Auto-generated method stub
        return true;
    }

    @Override
    public void doCmd(String word) {
        // TODO Auto-generated method stub
        super.doCmd(word);
    }


}
复制代码
 

HandlerGo类

复制代码
package demo02.clock.chengbao;

public class HandlerGo extends Handler {


    HandlerGo(Game game) {
        super(game);
        // TODO Auto-generated constructor stub
    }

    @Override
    public void doCmd(String word) {
        // TODO Auto-generated method stub
        game.goRoom(word);
    }

}
复制代码
 

HandlerHelp类

复制代码
package demo02.clock.chengbao;

public class HandlerHelp extends Handler {


    HandlerHelp(Game game) {
        super(game);
        // TODO Auto-generated constructor stub
    }

    @Override
    public void doCmd(String word) {
        System.out.println("迷路了吗？你可以做的命令有：go bye help");
        System.out.println("如：\tgo east");
    }

}
复制代码
Room类

复制代码
package demo02.clock.chengbao;

import java.util.HashMap;

public class Room {
    private String description;
    private HashMap<String,Room> exits=new HashMap<String,Room>();

    public Room(String description)
    {
        this.description = description;
    }

    public void setExit(String dir,Room room)
    {
        exits.put(dir, room);
    }

    @Override
    public String toString()
    {
        return description;
    }
    public String getExitDesc()
    {
        StringBuffer ret=new StringBuffer();
        for(String dir :exits.keySet())
        {
            ret.append(dir);
            ret.append(" ");
        }
        return ret.toString();
    }
    public Room getExit(String direction)
    {
        return exits.get(direction);
    }
}


package demo02.clock.chengbao;

public class HandlerHelp extends Handler {


    HandlerHelp(Game game) {
        super(game);
        // TODO Auto-generated constructor stub
}

    @Override
public void doCmd(String word) {
        System.out.println("迷路了吗？你可以做的命令有：go bye help");
        System.out.println("如：\tgo east");
    }

}
