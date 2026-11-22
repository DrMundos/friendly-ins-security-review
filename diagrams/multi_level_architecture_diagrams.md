<?xml version="1.0" encoding="UTF-8"?>
<mxfile host="app.diagrams.net" modified="2026-11-19T07:16:00.000Z" agent="Mozilla/5.0" version="21.1.2" etag="friendly_ins_full_hld_lld" type="device">

  <!-- TAB 1: PART A - HLD (High-Level System & Business Architecture) -->
  <diagram id="part_a_hld" name="Part A - HLD Architecture">
    <mxGraphModel dx="1800" dy="1100" grid="1" gridSize="10" guides="1" tooltips="1" connect="1" arrows="1" fold="1" page="1" pageScale="1" pageWidth="1800" pageHeight="1100" math="0" shadow="0">
      <root>
        <mxCell id="a_hld_0" />
        <mxCell id="a_hld_1" parent="a_hld_0" />

        <mxCell id="a_hld_title" value="Part A — High-Level Architecture (HLD): friendly_ins Ecosystem (ClaimFlow v2 &amp; RiskLens)" style="text;html=1;strokeColor=none;fillColor=none;align=center;verticalAlign=middle;whiteSpace=wrap;rounded=0;fontStyle=1;fontSize=18;" vertex="1" parent="a_hld_1">
          <mxGeometry x="40" y="20" width="1720" height="36" as="geometry" />
        </mxCell>

        <mxCell id="act_policyholders" value="420,000 Policyholders (US &amp; EU)&lt;br&gt;Auto, Home, Travel, Health&lt;br&gt;~9,000 Claims/Month (3x storm spikes)" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;fontStyle=1;fontSize=11;" vertex="1" parent="a_hld_1">
          <mxGeometry x="60" y="90" width="280" height="80" as="geometry" />
        </mxCell>

        <mxCell id="act_brokers" value="35 External Broker Agencies&lt;br&gt;Underwriting, Quotes, Policies&lt;br&gt;Uses RiskLens &amp; Broker Copilot" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;fontStyle=1;fontSize=11;" vertex="1" parent="a_hld_1">
          <mxGeometry x="400" y="90" width="280" height="80" as="geometry" />
        </mxCell>

        <mxCell id="act_staff" value="~45 Engineers &amp; Contractors (dev-admin)&lt;br&gt;Support Agents &amp; Underwriters&lt;br&gt;Root Password in Shared 1Password" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#f8cecc;strokeColor=#b85450;fontStyle=1;fontSize=11;" vertex="1" parent="a_hld_1">
          <mxGeometry x="740" y="90" width="320" height="80" as="geometry" />
        </mxCell>

        <mxCell id="act_github" value="GitHub &amp; GitHub Actions CI/CD&lt;br&gt;Static IAM Key (ci-deployer, since 2021)&lt;br&gt;pull_request_target Trigger &amp; Auto DB Migrations" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#e1d5e7;strokeColor=#9673a6;fontStyle=1;fontSize=11;" vertex="1" parent="a_hld_1">
          <mxGeometry x="1120" y="90" width="320" height="80" as="geometry" />
        </mxCell>

        <mxCell id="hld_aws_box" value="Single AWS Account (Region: us-east-1) — Shared Across Dev, Staging &amp; Prod (No Account Isolation)" style="swimlane;whiteSpace=wrap;html=1;fillColor=#f5f5f5;fontColor=#222222;strokeColor=#555555;fontStyle=1;fontSize=14;" vertex="1" parent="a_hld_1">
          <mxGeometry x="60" y="210" width="1680" height="640" as="geometry" />
        </mxCell>

        <mxCell id="hld_claimflow" value="ClaimFlow Product&lt;br&gt;Client Portal (React) + Adjudication Engine&lt;br&gt;v2 Target: 40% Auto-Approval &lt; $5k in &lt; 1hr&lt;br&gt;Features: ClaimAssist AI, View as Customer" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#ffe6cc;strokeColor=#d79b00;fontStyle=1;fontSize=12;" vertex="1" parent="hld_aws_box">
          <mxGeometry x="50" y="60" width="380" height="120" as="geometry" />
        </mxCell>

        <mxCell id="hld_risklens" value="RiskLens Product&lt;br&gt;Underwriting &amp; Broker Platform&lt;br&gt;Broker APIs, Quotes, Broker Copilot (RAG)&lt;br&gt;Feeds Policy Data to Core DB" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#ffe6cc;strokeColor=#d79b00;fontStyle=1;fontSize=12;" vertex="1" parent="hld_aws_box">
          <mxGeometry x="480" y="60" width="380" height="120" as="geometry" />
        </mxCell>

        <mxCell id="hld_compute" value="AWS Compute &amp; ML Layer&lt;br&gt;ECS Fargate (Node.js/Express) &amp; EKS (Python/FastAPI)&lt;br&gt;Amazon SageMaker &amp; Import Worker (Public Subnet)" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#e1d5e7;strokeColor=#9673a6;fontStyle=1;fontSize=12;" vertex="1" parent="hld_aws_box">
          <mxGeometry x="910" y="60" width="380" height="120" as="geometry" />
        </mxCell>

        <mxCell id="hld_sec_obs" value="Observability, IAM &amp; Security Controls&lt;br&gt;CloudWatch (Never Expire logs, PII/PHI &amp; prompts)&lt;br&gt;CloudTrail (us-east-1 only) | GuardDuty &amp; SecHub OFF&lt;br&gt;WAF only on 1 CloudFront in Count Mode" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#f8cecc;strokeColor=#b85450;fontStyle=1;fontSize=11;" vertex="1" parent="hld_aws_box">
          <mxGeometry x="1320" y="60" width="330" height="120" as="geometry" />
        </mxCell>

        <mxCell id="hld_data_stores" value="Data Stores &amp; Search Layer&lt;br&gt;1. RDS PostgreSQL (Users, Claims, Policies, IBANs; Staging Public + Prod Clone)&lt;br&gt;2. Amazon S3 (Claim Documents PDFs/Invoices + S3 Data Lake)&lt;br&gt;3. Amazon Redshift (Analytics Warehouse - Unmasked Nightly ETL)&lt;br&gt;4. Amazon OpenSearch (Shared RAG Index for Broker Copilot)" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#d5e8d4;strokeColor=#82b366;fontStyle=1;fontSize=12;" vertex="1" parent="hld_aws_box">
          <mxGeometry x="50" y="250" width="1600" height="150" as="geometry" />
        </mxCell>

        <mxCell id="hld_crown_jewels" value="Crown Jewels &amp; Regulatory Scope (GDPR &amp; HIPAA)&lt;br&gt;PII: Names, Addresses, Govt IDs, SSNs  |  PHI: Medical Records, Psychiatric Notes, Diagnoses  |  Financial: IBANs, Payouts, Payment Keys" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#fff2cc;strokeColor=#d6b656;fontStyle=1;fontSize=12;" vertex="1" parent="hld_aws_box">
          <mxGeometry x="50" y="450" width="1600" height="90" as="geometry" />
        </mxCell>

        <mxCell id="ext_payfast" value="PayFast (Payment Gateway)&lt;br&gt;Processes payouts &amp; sends webhook callbacks&lt;br&gt;(POST /api/webhooks/payfast)" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#f8cecc;strokeColor=#b85450;fontStyle=1;fontSize=11;" vertex="1" parent="a_hld_1">
          <mxGeometry x="140" y="890" width="340" height="80" as="geometry" />
        </mxCell>

        <mxCell id="ext_novaai" value="NovaAI (External LLM / AI Service)&lt;br&gt;Powers ClaimAssist OCR &amp; AI adjudication&lt;br&gt;Receives extracted document text" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#fff2cc;strokeColor=#d6b656;fontStyle=1;fontSize=11;" vertex="1" parent="a_hld_1">
          <mxGeometry x="620" y="890" width="340" height="80" as="geometry" />
        </mxCell>

        <mxCell id="ext_chartwise" value="ChartWise (External BI Vendor)&lt;br&gt;BI analytics partner (PoC ended ~5 months ago)&lt;br&gt;Accesses analytics/warehouse data" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#f8cecc;strokeColor=#b85450;fontStyle=1;fontSize=11;" vertex="1" parent="a_hld_1">
          <mxGeometry x="1100" y="890" width="360" height="80" as="geometry" />
        </mxCell>

        <mxCell id="ah_e1" edge="1" source="act_policyholders" target="hld_claimflow" parent="a_hld_1"><mxGeometry relative="1" as="geometry" /></mxCell>
        <mxCell id="ah_e2" edge="1" source="act_brokers" target="hld_risklens" parent="a_hld_1"><mxGeometry relative="1" as="geometry" /></mxCell>
        <mxCell id="ah_e3" edge="1" source="act_staff" target="hld_sec_obs" parent="a_hld_1"><mxGeometry relative="1" as="geometry" /></mxCell>
        <mxCell id="ah_e4" edge="1" source="act_github" target="hld_compute" parent="a_hld_1"><mxGeometry relative="1" as="geometry" /></mxCell>
        <mxCell id="ah_e5" edge="1" source="hld_claimflow" target="hld_compute" parent="hld_aws_box"><mxGeometry relative="1" as="geometry" /></mxCell>
        <mxCell id="ah_e6" edge="1" source="hld_risklens" target="hld_compute" parent="hld_aws_box"><mxGeometry relative="1" as="geometry" /></mxCell>
        <mxCell id="ah_e7" edge="1" source="hld_compute" target="hld_data_stores" parent="hld_aws_box"><mxGeometry relative="1" as="geometry" /></mxCell>
        <mxCell id="ah_e8" edge="1" source="hld_data_stores" target="hld_crown_jewels" parent="hld_aws_box"><mxGeometry relative="1" as="geometry" /></mxCell>
        <mxCell id="ah_e9" edge="1" source="ext_payfast" target="hld_claimflow" parent="a_hld_1"><mxGeometry relative="1" as="geometry" /></mxCell>
        <mxCell id="ah_e10" edge="1" source="hld_compute" target="ext_novaai" parent="a_hld_1"><mxGeometry relative="1" as="geometry" /></mxCell>
        <mxCell id="ah_e11" edge="1" source="hld_data_stores" target="ext_chartwise" parent="a_hld_1"><mxGeometry relative="1" as="geometry" /></mxCell>
      </root>
    </mxGraphModel>
  </diagram>

  <!-- TAB 2: PART A - LLD (Low-Level Technical Components & Connections) -->
  <diagram id="part_a_lld" name="Part A - LLD AWS &amp; App Wiring">
    <mxGraphModel dx="1900" dy="1200" grid="1" gridSize="10" guides="1" tooltips="1" connect="1" arrows="1" fold="1" page="1" pageScale="1" pageWidth="1900" pageHeight="1200" math="0" shadow="0">
      <root>
        <mxCell id="a_lld_0" />
        <mxCell id="a_lld_1" parent="a_lld_0" />

        <mxCell id="a_lld_title" value="Part A — Low-Level Architecture (LLD): Exact AWS Components, Subnets, Flows &amp; Connections" style="text;html=1;strokeColor=none;fillColor=none;align=center;verticalAlign=middle;whiteSpace=wrap;rounded=0;fontStyle=1;fontSize=18;" vertex="1" parent="a_lld_1">
          <mxGeometry x="40" y="20" width="1820" height="36" as="geometry" />
        </mxCell>

        <mxCell id="lld_vpc" value="AWS Single VPC (us-east-1) — Shared Dev / Staging / Prod Network" style="swimlane;whiteSpace=wrap;html=1;fillColor=#f5f5f5;strokeColor=#444444;fontStyle=1;fontSize=14;" vertex="1" parent="a_lld_1">
          <mxGeometry x="50" y="70" width="1800" height="860" as="geometry" />
        </mxCell>

        <mxCell id="lld_pub_sub" value="Public Subnet (Internet-Facing)" style="swimlane;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;fontStyle=1;fontSize=12;" vertex="1" parent="lld_vpc">
          <mxGeometry x="30" y="40" width="1740" height="130" as="geometry" />
        </mxCell>

        <mxCell id="lld_cloudfront_waf" value="Amazon CloudFront + AWS WAF&lt;br&gt;(WAF only on 1 CloudFront; Rules set to Count, not Block)" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#ffffff;strokeColor=#6c8ebf;fontSize=11;fontStyle=1;" vertex="1" parent="lld_pub_sub">
          <mxGeometry x="30" y="35" width="380" height="75" as="geometry" />
        </mxCell>

        <mxCell id="lld_alb" value="Application Load Balancer (ALB)&lt;br&gt;Routes ClaimFlow &amp; RiskLens traffic" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#ffffff;strokeColor=#6c8ebf;fontSize=11;fontStyle=1;" vertex="1" parent="lld_pub_sub">
          <mxGeometry x="450" y="35" width="350" height="75" as="geometry" />
        </mxCell>

        <mxCell id="lld_import_worker" value="Import Worker (Public Subnet)&lt;br&gt;SSH Port 22 Open to 0.0.0.0/0&lt;br&gt;IMDSv1 Enabled (Metadata Risk)" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#f8cecc;strokeColor=#b85450;fontSize=11;fontStyle=1;" vertex="1" parent="lld_pub_sub">
          <mxGeometry x="840" y="35" width="420" height="75" as="geometry" />
        </mxCell>

        <mxCell id="lld_staging_db" value="Staging RDS DB (Publicly Accessible!)&lt;br&gt;Weekly Full Prod Restore (Unmasked PII/PHI)&lt;br&gt;Same Password as Production" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#f8cecc;strokeColor=#b85450;fontSize=11;fontStyle=1;" vertex="1" parent="lld_pub_sub">
          <mxGeometry x="1300" y="35" width="410" height="75" as="geometry" />
        </mxCell>

        <mxCell id="lld_app_sub" value="Private Application Subnet — Containers, Microservices &amp; AI Services" style="swimlane;whiteSpace=wrap;html=1;fillColor=#e1d5e7;strokeColor=#9673a6;fontStyle=1;fontSize=12;" vertex="1" parent="lld_vpc">
          <mxGeometry x="30" y="195" width="1740" height="190" as="geometry" />
        </mxCell>

        <mxCell id="lld_ecs_claimflow" value="Amazon ECS Fargate (Node.js / Express)&lt;br&gt;- ClaimFlow API &amp; Adjudication Engine&lt;br&gt;- POST /api/webhooks/payfast (No HMAC)&lt;br&gt;- POST /api/support/impersonate &amp; PUT /bank-details&lt;br&gt;- Auto DB migrations on container start" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#ffffff;strokeColor=#9673a6;fontSize=11;" vertex="1" parent="lld_app_sub">
          <mxGeometry x="30" y="35" width="410" height="135" as="geometry" />
        </mxCell>

        <mxCell id="lld_eks_copilot" value="Amazon EKS (Python / FastAPI)&lt;br&gt;- RiskLens API &amp; Broker Copilot RAG&lt;br&gt;- Queries OpenSearch without broker_id filter" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#ffffff;strokeColor=#9673a6;fontSize=11;" vertex="1" parent="lld_app_sub">
          <mxGeometry x="470" y="35" width="410" height="135" as="geometry" />
        </mxCell>

        <mxCell id="lld_claimassist" value="ClaimAssist OCR &amp; AI Adjudication&lt;br&gt;- Reads S3 docs (invoices, medical PDFs)&lt;br&gt;- Raw OCR text concatenated into LLM prompt&lt;br&gt;- Calls NovaAI &amp; Amazon SageMaker" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#fff2cc;strokeColor=#d6b656;fontSize=11;" vertex="1" parent="lld_app_sub">
          <mxGeometry x="910" y="35" width="410" height="135" as="geometry" />
        </mxCell>

        <mxCell id="lld_etl_job" value="Nightly ETL Pipeline Job&lt;br&gt;- Pulls raw tables from RDS PostgreSQL&lt;br&gt;- Replicates unmasked PII/PHI to S3 &amp; Redshift" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#fff2cc;strokeColor=#d6b656;fontSize=11;" vertex="1" parent="lld_app_sub">
          <mxGeometry x="1350" y="35" width="360" height="135" as="geometry" />
        </mxCell>

        <mxCell id="lld_data_sub" value="Data Stores, Search Index &amp; Secrets" style="swimlane;whiteSpace=wrap;html=1;fillColor=#d5e8d4;strokeColor=#82b366;fontStyle=1;fontSize=12;" vertex="1" parent="lld_vpc">
          <mxGeometry x="30" y="410" width="1740" height="185" as="geometry" />
        </mxCell>

        <mxCell id="lld_rds_prod" value="Amazon RDS PostgreSQL (Production)&lt;br&gt;Users, Claims, Policies, Bank IBANs, Payout Status" style="shape=cylinder3;whiteSpace=wrap;html=1;boundedLbl=1;backgroundFill=1;fillColor=#ffffff;strokeColor=#82b366;fontSize=11;" vertex="1" parent="lld_data_sub">
          <mxGeometry x="30" y="35" width="380" height="125" as="geometry" />
        </mxCell>

        <mxCell id="lld_s3_docs_lake" value="Amazon S3 Buckets&lt;br&gt;- Document Bucket (Pre-signed URL uploads, PII/PHI)&lt;br&gt;- S3 Data Lake (Nightly ETL output)" style="shape=cylinder3;whiteSpace=wrap;html=1;boundedLbl=1;backgroundFill=1;fillColor=#ffffff;strokeColor=#82b366;fontSize=11;" vertex="1" parent="lld_data_sub">
          <mxGeometry x="450" y="35" width="410" height="125" as="geometry" />
        </mxCell>

        <mxCell id="lld_redshift" value="Amazon Redshift&lt;br&gt;Analytics &amp; BI Warehouse&lt;br&gt;Holds unmasked PII/PHI; ChartWise connected" style="shape=cylinder3;whiteSpace=wrap;html=1;boundedLbl=1;backgroundFill=1;fillColor=#ffffff;strokeColor=#82b366;fontSize=11;" vertex="1" parent="lld_data_sub">
          <mxGeometry x="900" y="35" width="380" height="125" as="geometry" />
        </mxCell>

        <mxCell id="lld_opensearch" value="Amazon OpenSearch&lt;br&gt;Single shared index for Broker Copilot RAG&lt;br&gt;Multi-tenant policy &amp; claim embeddings" style="shape=cylinder3;whiteSpace=wrap;html=1;boundedLbl=1;backgroundFill=1;fillColor=#ffffff;strokeColor=#82b366;fontSize=11;" vertex="1" parent="lld_data_sub">
          <mxGeometry x="1320" y="35" width="390" height="125" as="geometry" />
        </mxCell>

        <mxCell id="lld_ops_sub" value="AWS IAM, Secrets, Logging &amp; Security Monitoring" style="swimlane;whiteSpace=wrap;html=1;fillColor=#f8cecc;strokeColor=#b85450;fontStyle=1;fontSize=12;" vertex="1" parent="lld_vpc">
          <mxGeometry x="30" y="620" width="1740" height="210" as="geometry" />
        </mxCell>

        <mxCell id="lld_iam" value="AWS IAM &amp; Root Account&lt;br&gt;- ~45 users/contractors in dev-admin (AdministratorAccess)&lt;br&gt;- MFA optional; Root pass in shared 1Password&lt;br&gt;- Static IAM user ci-deployer (Admin key since 2021)" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#ffffff;strokeColor=#b85450;fontSize=11;" vertex="1" parent="lld_ops_sub">
          <mxGeometry x="30" y="35" width="540" height="150" as="geometry" />
        </mxCell>

        <mxCell id="lld_cloudwatch" value="Amazon CloudWatch Logs&lt;br&gt;- Retention: Never Expire&lt;br&gt;- Logs full HTTP request/response bodies &amp; LLM prompts&lt;br&gt;- Contains PII/PHI; readable by ~45 admins" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#ffffff;strokeColor=#b85450;fontSize=11;" vertex="1" parent="lld_ops_sub">
          <mxGeometry x="610" y="35" width="540" height="150" as="geometry" />
        </mxCell>

        <mxCell id="lld_cloudtrail_sec" value="CloudTrail, GuardDuty, Security Hub &amp; Secrets&lt;br&gt;- AWS CloudTrail enabled ONLY in us-east-1&lt;br&gt;- GuardDuty &amp; Security Hub DISABLED (cost saving)&lt;br&gt;- Secrets / API keys for PayFast &amp; NovaAI" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#ffffff;strokeColor=#b85450;fontSize=11;" vertex="1" parent="lld_ops_sub">
          <mxGeometry x="1190" y="35" width="520" height="150" as="geometry" />
        </mxCell>

        <mxCell id="lld_ext_gh" value="GitHub Actions&lt;br&gt;pull_request_target + ci-deployer key" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#e1d5e7;strokeColor=#9673a6;fontStyle=1;fontSize=11;" vertex="1" parent="a_lld_1">
          <mxGeometry x="80" y="960" width="320" height="75" as="geometry" />
        </mxCell>

        <mxCell id="lld_ext_payfast" value="PayFast Gateway&lt;br&gt;Webhook POST /api/webhooks/payfast" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#f8cecc;strokeColor=#b85450;fontStyle=1;fontSize=11;" vertex="1" parent="a_lld_1">
          <mxGeometry x="520" y="960" width="360" height="75" as="geometry" />
        </mxCell>

        <mxCell id="lld_ext_nova" value="NovaAI LLM API&lt;br&gt;ClaimAssist &amp; Copilot inference" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#fff2cc;strokeColor=#d6b656;fontStyle=1;fontSize=11;" vertex="1" parent="a_lld_1">
          <mxGeometry x="1000" y="960" width="360" height="75" as="geometry" />
        </mxCell>

        <mxCell id="lld_ext_chartwise" value="ChartWise BI&lt;br&gt;External BI analytics consumer" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#f8cecc;strokeColor=#b85450;fontStyle=1;fontSize=11;" vertex="1" parent="a_lld_1">
          <mxGeometry x="1480" y="960" width="340" height="75" as="geometry" />
        </mxCell>

        <mxCell id="al_e1" edge="1" source="lld_cloudfront_waf" target="lld_alb" parent="lld_pub_sub"><mxGeometry relative="1" as="geometry" /></mxCell>
        <mxCell id="al_e2" edge="1" source="lld_alb" target="lld_ecs_claimflow" parent="lld_vpc"><mxGeometry relative="1" as="geometry" /></mxCell>
        <mxCell id="al_e3" edge="1" source="lld_alb" target="lld_eks_copilot" parent="lld_vpc"><mxGeometry relative="1" as="geometry" /></mxCell>
        <mxCell id="al_e4" edge="1" source="lld_ecs_claimflow" target="lld_claimassist" parent="lld_app_sub"><mxGeometry relative="1" as="geometry" /></mxCell>
        <mxCell id="al_e5" edge="1" source="lld_ecs_claimflow" target="lld_rds_prod" parent="lld_vpc"><mxGeometry relative="1" as="geometry" /></mxCell>
        <mxCell id="al_e6" edge="1" source="lld_claimassist" target="lld_s3_docs_lake" parent="lld_vpc"><mxGeometry relative="1" as="geometry" /></mxCell>
        <mxCell id="al_e7" edge="1" source="lld_eks_copilot" target="lld_opensearch" parent="lld_vpc"><mxGeometry relative="1" as="geometry" /></mxCell>
        <mxCell id="al_e8" edge="1" source="lld_rds_prod" target="lld_etl_job" parent="lld_vpc"><mxGeometry relative="1" as="geometry" /></mxCell>
        <mxCell id="al_e9" edge="1" source="lld_etl_job" target="lld_s3_docs_lake" parent="lld_vpc"><mxGeometry relative="1" as="geometry" /></mxCell>
        <mxCell id="al_e10" edge="1" source="lld_etl_job" target="lld_redshift" parent="lld_vpc"><mxGeometry relative="1" as="geometry" /></mxCell>
        <mxCell id="al_e11" edge="1" source="lld_rds_prod" target="lld_staging_db" parent="lld_vpc"><mxGeometry relative="1" as="geometry" /></mxCell>
        <mxCell id="al_e12" edge="1" source="lld_ext_gh" target="lld_ecs_claimflow" parent="a_lld_1"><mxGeometry relative="1" as="geometry" /></mxCell>
        <mxCell id="al_e13" edge="1" source="lld_ext_payfast" target="lld_ecs_claimflow" parent="a_lld_1"><mxGeometry relative="1" as="geometry" /></mxCell>
        <mxCell id="al_e14" edge="1" source="lld_claimassist" target="lld_ext_nova" parent="a_lld_1"><mxGeometry relative="1" as="geometry" /></mxCell>
        <mxCell id="al_e15" edge="1" source="lld_redshift" target="lld_ext_chartwise" parent="a_lld_1"><mxGeometry relative="1" as="geometry" /></mxCell>
      </root>
    </mxGraphModel>
  </diagram>

  <!-- TAB 3: PART B - LLD (Vulnerabilities, Attack Paths & Mitigations) -->
  <diagram id="part_b_lld" name="Part B - LLD Risk &amp; Attack Paths">
    <mxGraphModel dx="1900" dy="1200" grid="1" gridSize="10" guides="1" tooltips="1" connect="1" arrows="1" fold="1" page="1" pageScale="1" pageWidth="1900" pageHeight="1200" math="0" shadow="0">
      <root>
        <mxCell id="b_lld_0" />
        <mxCell id="b_lld_1" parent="b_lld_0" />

        <mxCell id="b_lld_title" value="Part B — Low-Level Threat &amp; Mitigation Architecture (R-01 to R-06)" style="text;html=1;strokeColor=none;fillColor=none;align=center;verticalAlign=middle;whiteSpace=wrap;rounded=0;fontStyle=1;fontSize=18;" vertex="1" parent="b_lld_1">
          <mxGeometry x="40" y="20" width="1820" height="36" as="geometry" />
        </mxCell>

        <mxCell id="b_r01" value="R-01 [CRITICAL | Launch Blocker]&lt;br&gt;POST /api/webhooks/payfast&lt;br&gt;Issue: No auth / no HMAC check&lt;br&gt;Attack: Spoofed payment marks unpaid claim PAID&lt;br&gt;Quick: ALB/WAF PayFast IP allowlist&lt;br&gt;Fix: HMAC-SHA256 + DB state check" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#f8cecc;strokeColor=#b85450;fontSize=11;fontStyle=1;" vertex="1" parent="b_lld_1">
          <mxGeometry x="50" y="90" width="560" height="160" as="geometry" />
        </mxCell>

        <mxCell id="b_r02" value="R-02 [CRITICAL | Launch Blocker]&lt;br&gt;ClaimAssist AI Adjudication (&lt; $5k in &lt; 1hr)&lt;br&gt;Issue: Raw OCR text merged into LLM prompt&lt;br&gt;Attack: Indirect prompt injection in PDF/invoice&lt;br&gt;Quick: Feature Flag OFF (disable auto payout)&lt;br&gt;Fix: XML delimiters + code limit checks + schema check" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#f8cecc;strokeColor=#b85450;fontSize=11;fontStyle=1;" vertex="1" parent="b_lld_1">
          <mxGeometry x="670" y="90" width="560" height="160" as="geometry" />
        </mxCell>

        <mxCell id="b_r03" value="R-03 [CRITICAL | Launch Blocker]&lt;br&gt;Broker Copilot RAG (Amazon OpenSearch)&lt;br&gt;Issue: Shared index without broker_id filter&lt;br&gt;Attack: Broker queries other brokers' claims/PHI&lt;br&gt;Quick: Restrict to internal underwriters only&lt;br&gt;Fix: Mandatory JWT broker_id pre-filtering" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#f8cecc;strokeColor=#b85450;fontSize=11;fontStyle=1;" vertex="1" parent="b_lld_1">
          <mxGeometry x="1290" y="90" width="560" height="160" as="geometry" />
        </mxCell>

        <mxCell id="b_r04" value="R-04 [CRITICAL | Launch Blocker]&lt;br&gt;Support 'View as Customer' Impersonation&lt;br&gt;Issue: Full write privileges; no customer OTP&lt;br&gt;Attack: Overwrite payout IBAN &amp; steal claim funds&lt;br&gt;Quick: Read-only impersonation (block POST/PUT/DEL)&lt;br&gt;Fix: RBAC + customer OTP + actor_id/subject_id logs" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#f8cecc;strokeColor=#b85450;fontSize=11;fontStyle=1;" vertex="1" parent="b_lld_1">
          <mxGeometry x="50" y="300" width="560" height="160" as="geometry" />
        </mxCell>

        <mxCell id="b_r05" value="R-05 [CRITICAL | Launch Blocker]&lt;br&gt;Single AWS Account &amp; ~45 Admins (dev-admin)&lt;br&gt;Issue: Shared Dev/Stage/Prod VPC; MFA optional&lt;br&gt;Attack: Phished dev/contractor compromises Prod&lt;br&gt;Quick: Deny IAM without MFA; remove contractor admin&lt;br&gt;Fix: AWS Organizations multi-account + IAM Identity Center" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#f8cecc;strokeColor=#b85450;fontSize=11;fontStyle=1;" vertex="1" parent="b_lld_1">
          <mxGeometry x="670" y="300" width="560" height="160" as="geometry" />
        </mxCell>

        <mxCell id="b_r06" value="R-06 [HIGH | Before Launch / Urgent]&lt;br&gt;Nightly ETL, Redshift &amp; CloudWatch Logs&lt;br&gt;Issue: Unmasked PII/PHI sync + Never Expire logs&lt;br&gt;Attack: Broad admin/BI (ChartWise) access &amp; GDPR breach&lt;br&gt;Quick: 30-day log retention, scrub bodies, revoke BI&lt;br&gt;Fix: ETL masking/tokenization + cross-store GDPR delete" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#fff2cc;strokeColor=#d6b656;fontSize=11;fontStyle=1;" vertex="1" parent="b_lld_1">
          <mxGeometry x="1290" y="300" width="560" height="160" as="geometry" />
        </mxCell>

        <mxCell id="b_impact" value="Compounded Attack Paths &amp; Crown Jewels Impact&lt;br&gt;1. Financial Theft: Fake PAID webhook (R-01) + Prompt injection (R-02) + IBAN swap (R-04)&lt;br&gt;2. Data Breach &amp; GDPR/HIPAA Violation: Cross-tenant RAG leak (R-03) + Unmasked ETL/CloudWatch (R-06)&lt;br&gt;3. Full Cloud Takeover: Single AWS account + ~45 admins without MFA (R-05)" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#e1d5e7;strokeColor=#9673a6;fontSize=12;fontStyle=1;" vertex="1" parent="b_lld_1">
          <mxGeometry x="50" y="530" width="1800" height="140" as="geometry" />
        </mxCell>

        <mxCell id="bl_1" edge="1" source="b_r01" target="b_impact" parent="b_lld_1"><mxGeometry relative="1" as="geometry" /></mxCell>
        <mxCell id="bl_2" edge="1" source="b_r02" target="b_impact" parent="b_lld_1"><mxGeometry relative="1" as="geometry" /></mxCell>
        <mxCell id="bl_3" edge="1" source="b_r03" target="b_impact" parent="b_lld_1"><mxGeometry relative="1" as="geometry" /></mxCell>
        <mxCell id="bl_4" edge="1" source="b_r04" target="b_impact" parent="b_lld_1"><mxGeometry relative="1" as="geometry" /></mxCell>
        <mxCell id="bl_5" edge="1" source="b_r05" target="b_impact" parent="b_lld_1"><mxGeometry relative="1" as="geometry" /></mxCell>
        <mxCell id="bl_6" edge="1" source="b_r06" target="b_impact" parent="b_lld_1"><mxGeometry relative="1" as="geometry" /></mxCell>
      </root>
    </mxGraphModel>
  </diagram>

  <!-- TAB 4: PART C - HLD (CISO Target State & Governance Roadmap) -->
  <diagram id="part_c_hld" name="Part C - HLD Target State &amp; CISO">
    <mxGraphModel dx="1900" dy="1200" grid="1" gridSize="10" guides="1" tooltips="1" connect="1" arrows="1" fold="1" page="1" pageScale="1" pageWidth="1900" pageHeight="1200" math="0" shadow="0">
      <root>
        <mxCell id="c_hld_0" />
        <mxCell id="c_hld_1" parent="c_hld_0" />

        <mxCell id="c_hld_title" value="Part C — CISO Target State Architecture &amp; Prioritized Roadmap (HLD)" style="text;html=1;strokeColor=none;fillColor=none;align=center;verticalAlign=middle;whiteSpace=wrap;rounded=0;fontStyle=1;fontSize=18;" vertex="1" parent="c_hld_1">
          <mxGeometry x="40" y="20" width="1820" height="36" as="geometry" />
        </mxCell>

        <mxCell id="c_org_boundary" value="AWS Organizations — Multi-Account Target Architecture &amp; IAM Identity Center (Mandatory MFA)" style="swimlane;whiteSpace=wrap;html=1;fillColor=#f5f5f5;strokeColor=#444444;fontStyle=1;fontSize=14;" vertex="1" parent="c_hld_1">
          <mxGeometry x="50" y="80" width="1800" height="580" as="geometry" />
        </mxCell>

        <mxCell id="c_prod_acc" value="Production Account (Isolated)&lt;br&gt;- WAF in Block Mode + ALB&lt;br&gt;- HMAC-SHA256 PayFast Webhook Check&lt;br&gt;- ClaimAssist Guardrails + Code Limits&lt;br&gt;- OpenSearch broker_id Pre-Filtering&lt;br&gt;- Read-Only Impersonation + Customer OTP&lt;br&gt;- Private RDS PostgreSQL &amp; S3" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#d5e8d4;strokeColor=#82b366;fontStyle=1;fontSize=11;" vertex="1" parent="c_org_boundary">
          <mxGeometry x="40" y="50" width="540" height="480" as="geometry" />
        </mxCell>

        <mxCell id="c_sec_acc" value="Security &amp; Audit Account (Isolated)&lt;br&gt;- CloudWatch Logs (30-Day Retention)&lt;br&gt;- Scrubbed PII/PHI &amp; Prompts&lt;br&gt;- Multi-Region CloudTrail + GuardDuty&lt;br&gt;- Immutable actor_id / subject_id Logs" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;fontStyle=1;fontSize=11;" vertex="1" parent="c_org_boundary">
          <mxGeometry x="630" y="50" width="540" height="480" as="geometry" />
        </mxCell>

        <mxCell id="c_nonprod_acc" value="Staging / Dev / Analytics Account&lt;br&gt;- Staging DB Private &amp; Masked (No Prod Pass)&lt;br&gt;- Nightly ETL Masking / Tokenization&lt;br&gt;- ChartWise Access Revoked Until Hardened&lt;br&gt;- Short-lived SSO Roles (No Standing Admin)" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#ffe6cc;strokeColor=#d79b00;fontStyle=1;fontSize=11;" vertex="1" parent="c_org_boundary">
          <mxGeometry x="1220" y="50" width="540" height="480" as="geometry" />
        </mxCell>

        <mxCell id="c_decisions" value="Executive Decisions for CISO Sign-Off:&lt;br&gt;1. Launch Blockers (R-01 to R-05): Pause v2 public release (~2 weeks) until critical blockers are resolved.&lt;br&gt;2. Payout Safeguard (R-02): Toggle Feature Flag OFF for automated payouts; require finance sign-off while testing AI in live traffic.&lt;br&gt;3. Broker Copilot (R-03): Restrict to internal underwriters until tenant isolation is verified; 30/90-day GDPR deletion &amp; ETL masking." style="rounded=1;whiteSpace=wrap;html=1;fillColor=#e1d5e7;strokeColor=#9673a6;fontStyle=1;fontSize=12;" vertex="1" parent="c_hld_1">
          <mxGeometry x="50" y="700" width="1800" height="160" as="geometry" />
        </mxCell>
      </root>
    </mxGraphModel>
  </diagram>

  <!-- TAB 5: PART D - LLD (Assumptions, R&D Artifacts & Verification) -->
  <diagram id="part_d_lld" name="Part D - LLD R&amp;D Verification">
    <mxGraphModel dx="1900" dy="1200" grid="1" gridSize="10" guides="1" tooltips="1" connect="1" arrows="1" fold="1" page="1" pageScale="1" pageWidth="1900" pageHeight="1200" math="0" shadow="0">
      <root>
        <mxCell id="d_lld_0" />
        <mxCell id="d_lld_1" parent="d_lld_0" />

        <mxCell id="d_lld_title" value="Part D — Assumptions, R&amp;D Artifact Requests &amp; Verification Flow (LLD)" style="text;html=1;strokeColor=none;fillColor=none;align=center;verticalAlign=middle;whiteSpace=wrap;rounded=0;fontStyle=1;fontSize=18;" vertex="1" parent="d_lld_1">
          <mxGeometry x="40" y="20" width="1820" height="36" as="geometry" />
        </mxCell>

        <mxCell id="d_assump_box" value="Baseline Assumptions Made" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;fontStyle=1;fontSize=12;" vertex="1" parent="d_lld_1">
          <mxGeometry x="50" y="90" width="560" height="300" as="geometry" />
        </mxCell>

        <mxCell id="d_rd_box" value="Targeted R&amp;D Questions &amp; Code/Config Artifacts Requested&lt;br&gt;- R-01: PayFast HMAC enforcement &amp; webhook handler code&lt;br&gt;- R-02: OCR parsing &amp; ClaimAssist prompt template&lt;br&gt;- R-03: OpenSearch query builder &amp; broker_id mapping&lt;br&gt;- R-04: Impersonation middleware &amp; CloudWatch audit log sample&lt;br&gt;- R-05: Terraform/IaC, IAM policies, ci-deployer &amp; GitHub workflows&lt;br&gt;- R-06: CloudWatch retention config &amp; nightly ETL masking scripts" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#fff2cc;strokeColor=#d6b656;fontStyle=1;fontSize=11;" vertex="1" parent="d_lld_1">
          <mxGeometry x="670" y="90" width="580" height="300" as="geometry" />
        </mxCell>

        <mxCell id="d_verify_box" value="Verification &amp; Sign-Off Gates&lt;br&gt;- Negative tests on PayFast webhook (HTTP 401/403)&lt;br&gt;- Red-team prompt injection suite (0% unauthorized payouts)&lt;br&gt;- Cross-broker RAG query tests (0 cross-tenant leaks)&lt;br&gt;- Impersonation write-block tests (HTTP 403)&lt;br&gt;- IAM Access Analyzer (100% MFA) &amp; ETL/log PII scan" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#d5e8d4;strokeColor=#82b366;fontStyle=1;fontSize=11;" vertex="1" parent="d_lld_1">
          <mxGeometry x="1310" y="90" width="540" height="300" as="geometry" />
        </mxCell>
      </root>
    </mxGraphModel>
  </diagram>

</mxfile>