# journal_analysis
Sentiment analysis of text (journal) entries, aimed to help individuals identify behavior trends.   

import openai

def analyze_journal_entry(entry):
    # Generate prompt for analyzing journal entry
    prompt = f"Analyzing common themes in the journal entry:\n{entry}\n\nThemes:"

    # Set up OpenAI API credentials
    openai.api_key = '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'  # Replace with your OpenAI API key

    # Generate response using ChatGPT
    response = openai.Completion.create(
        engine="text-davinci-003",
        prompt=prompt,
        max_tokens=100,  # Adjust the number of tokens based on your desired response length
        n=3,  # Adjust the number of responses to retrieve
        stop=None,
        temperature=0.5,
        top_p=1.0,
        frequency_penalty=0.0,
        presence_penalty=0.0
    )

    # Extract the generated themes from the response
    themes = [choice['text'].strip() for choice in response.choices]

    return themes

def provide_suggestions(themes):
    suggestions = []

    for theme in themes:
        # Add custom logic to provide suggestions based on each theme
        if "work challenges" in theme:
            suggestions.append("1. Prioritize tasks and break them down into smaller, manageable steps.")
            suggestions.append("2. Consider seeking support or assistance from colleagues or supervisors.")
        elif "task completion" in theme:
            suggestions.append("1. Celebrate your achievements and acknowledge your progress.")
            suggestions.append("2. Reflect on the strategies or techniques that helped you successfully complete the project.")
        elif "focus and productivity" in theme:
            suggestions.append("1. Experiment with different productivity techniques, such as time-blocking or the Pomodoro Technique.")
            suggestions.append("2. Create a conducive work environment free from distractions.")
    
    return suggestions

# Example usage
journal_entry = "Today was a challenging day at work. I felt overwhelmed with tasks and struggled to stay focused. However, I managed to complete an important project and received positive feedback from my supervisor."

# Analyze the journal entry for common themes
themes = analyze_journal_entry(journal_entry)

# Provide suggestions based on the themes
suggestions = provide_suggestions(themes)

# Display the suggestions
print("Suggestions:")
if len(suggestions) > 0:
    for i, suggestion in enumerate(suggestions):
        print(f"{i+1}. {suggestion}")
else:
    print("No specific suggestions available for the mentioned themes.")
