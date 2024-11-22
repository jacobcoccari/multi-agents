import { MultiAgentOrchestrator, BedrockLLMAgent } from "multi-agent-orchestrator";

const orchestrator = new MultiAgentOrchestrator({
  config: {
    LOG_AGENT_CHAT: true,
    LOG_CLASSIFIER_CHAT: true,
    LOG_CLASSIFIER_RAW_OUTPUT: false,
    LOG_CLASSIFIER_OUTPUT: true,
    LOG_EXECUTION_TIMES: true,
  }
});

orchestrator.addAgent(
  new BedrockLLMAgent({
    name: "Legal Agent",
    description: "Specializes in legal matters including contract law, intellectual property, regulatory compliance, corporate law, international law, and legal documentation analysis.",
    streaming: true
  })
);

orchestrator.addAgent(
  new BedrockLLMAgent({
    name: "Finance Agent",
    description: "Focuses on financial topics such as investment strategies, market analysis, banking, cryptocurrency, personal finance, tax planning, and financial risk management.",
  })
);

const userId = "quickstart-user";
const sessionId = "quickstart-session";
const query = "How to conduct a vertical financial analysis on the balance sheet of a public company?";
console.log(`\nUser Query: ${query}`);

async function main() {
  try {
    const response = await orchestrator.routeRequest(query, userId, sessionId);
    console.log("\n** RESPONSE ** \n");
    console.log(`> Agent ID: ${response.metadata.agentId}`);
    console.log(`> Agent Name: ${response.metadata.agentName}`);
    console.log(`> User Input: ${response.metadata.userInput}`);
    console.log(`> User ID: ${response.metadata.userId}`);
    console.log(`> Session ID: ${response.metadata.sessionId}`);
    console.log(
      `> Additional Parameters:`,
      response.metadata.additionalParams
    );
    console.log(`\n> Response: `);
    // Stream the content
    for await (const chunk of response.output) {
      if (typeof chunk === "string") {
        process.stdout.write(chunk);
      } else {
        console.error("Received unexpected chunk type:", typeof chunk);
      }
    }
    console.log();
  } catch (error) {
    console.error("An error occurred:", error);
    // Here you could also add more specific error handling if needed
  }
}

main();