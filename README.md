# Task-2-Artificial-intelligence-chatbot
import java.util.*;
import java.util.regex.*;

class Response
{
    private Pattern pattern;
    private List<String> responses;

    public Response(String pattern, String... responses) 
    {
        this.pattern = Pattern.compile(pattern, Pattern.CASE_INSENSITIVE);
        this.responses = Arrays.asList(responses);
    }

    public boolean matches(String input)
    {
        Matcher matcher = pattern.matcher(input);
        return matcher.find();
    }

    public String getResponse() 
    {
        Random random = new Random();
        return responses.get(random.nextInt(responses.size()));
    }
}

class Chatbot
{
    private List<Response> responses;

    public Chatbot()
    {
        responses = new ArrayList<>();
        responses.add(new Response("hi|hello|hey", 
            "Hello!", "Hi there!", "Hey! How can I help you?"));
        responses.add(new Response("how are you or u", 
            "I'm doing well, thank you!", "I'm fine, how about you?"));
        responses.add(new Response("what is your name","what's ur name", 
            "My name is ChatBot.", "I'm ChatBot, nice to meet you!"));
        responses.add(new Response("bye|goodbye", 
            "Goodbye!", "See you later!", "Have a great day!"));
        responses.add(new Response("weather", 
            "I'm sorry, I don't have real-time weather information.", 
            "You might want to check a weather app for accurate information."));
        responses.add(new Response("joke", 
            "Why don't scientists trust atoms? Because they make up everything!",
            "What do you call a fake noodle? An impasta!"));
        responses.add(new Response("thank you", 
            "You're welcome!", "Glad I could help!", "My pleasure!"));
        responses.add(new Response("ok","well,have a good day","is there anything I can do to help u further with"));
        responses.add(new Response("what is java?","Java is a programming language which mainly follows object oriented "));
    }

    public String generateResponse(String input)
    {
        for (Response response : responses) 
        {
            if (response.matches(input)) 
            {
                return response.getResponse();
            }
        }
        return "I'm not sure how to respond to that. Can you try rephrasing?";
    }
}

public class Task4
{
    public static void main(String[] args) {
        Chatbot chatbot = new Chatbot();
        Scanner scanner = new Scanner(System.in);

        System.out.println("Chatbot: Hello! How can I assist you today? (Type 'bye' to exit)");

        while (true) 
        {
            System.out.print("You: ");
            String input = scanner.nextLine();

            if (input.equalsIgnoreCase("bye")) 
            {
                System.out.println("Chatbot: " + chatbot.generateResponse(input));
                break;
            }

            String response = chatbot.generateResponse(input);
            System.out.println("Chatbot: " + response);
        }

        scanner.close();
    }
}
