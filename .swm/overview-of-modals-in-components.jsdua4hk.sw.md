---
title: Overview of Modals in Components
---
# Overview of Modals in Components

Modals are used to display content in a layer above the main application, often requiring user interaction before returning to the main interface. They are implemented as React components and are styled using Emotion's <SwmToken path="static/app/components/modals/sudoModal.tsx" pos="2:2:2" line-data="import styled from &#39;@emotion/styled&#39;;">`styled`</SwmToken> function.

## Common Properties and Functions

Each modal component typically includes properties for rendering the modal's body, header, and footer, as well as functions for handling user actions such as form submissions or button clicks. Modals are used for various purposes, such as creating teams, suggesting projects, and managing integrations.

## Example: <SwmToken path="static/app/components/modals/sudoModal.tsx" pos="55:2:2" line-data="function SudoModal({">`SudoModal`</SwmToken>

<SwmToken path="static/app/components/modals/sudoModal.tsx" pos="55:2:2" line-data="function SudoModal({">`SudoModal`</SwmToken> handles user authentication by displaying forms for superuser access and managing the state of the authentication process.

<SwmSnippet path="/static/app/components/modals/sudoModal.tsx" line="55">

---

The <SwmToken path="static/app/components/modals/sudoModal.tsx" pos="55:2:2" line-data="function SudoModal({">`SudoModal`</SwmToken> function handles user authentication by displaying forms for superuser access and managing the state of the authentication process. It uses hooks like <SwmToken path="static/app/components/modals/sudoModal.tsx" pos="64:7:7" line-data="  const router = useRouter();">`useRouter`</SwmToken>, <SwmToken path="static/app/components/modals/sudoModal.tsx" pos="65:7:7" line-data="  const api = useApi();">`useApi`</SwmToken>, and <SwmToken path="static/app/components/modals/sudoModal.tsx" pos="20:3:3" line-data="import {useLocation} from &#39;sentry/utils/useLocation&#39;;">`useLocation`</SwmToken> to manage routing, API calls, and location data. The modal includes functions for handling form submissions, errors, and success states.

```tsx
function SudoModal({
  closeModal,
  isSuperuser,
  needsReload,
  retryRequest,
  Header,
  Body,
  closeButton,
}: Props) {
  const router = useRouter();
  const api = useApi();
  const [state, setState] = useState<State>({
    authenticators: [] as Authenticator[],
    error: false,
    errorType: '',
    showAccessForms: true,
    superuserAccessCategory: '',
    superuserReason: '',
    isLoading: true,
  });
```

---

</SwmSnippet>

<SwmSnippet path="/static/app/components/modals/createTeamModal.tsx" line="1">

---

The <SwmToken path="static/app/components/modals/createTeamModal.tsx" pos="15:2:2" line-data="function CreateTeamModal({Body, Header, ...props}: Props) {">`CreateTeamModal`</SwmToken> function is used for creating new teams within an organization. It includes a form for entering team details and handles the submission process.

```tsx
import {Fragment} from 'react';

import type {ModalRenderProps} from 'sentry/actionCreators/modal';
import {createTeam} from 'sentry/actionCreators/teams';
import CreateTeamForm from 'sentry/components/teams/createTeamForm';
import {t} from 'sentry/locale';
import type {Organization, Team} from 'sentry/types/organization';
import useApi from 'sentry/utils/useApi';

interface Props extends ModalRenderProps {
  organization: Organization;
  onClose?: (team: Team) => void;
}

function CreateTeamModal({Body, Header, ...props}: Props) {
  const {onClose, closeModal, organization} = props;
  const api = useApi();

  async function handleSubmit(
    data: {slug: string},
    onSuccess: Function,
```

---

</SwmSnippet>

## Example: SuggestProjectModal

`SuggestProjectModal` is used to suggest new projects to team members. It includes functionality for tracking user interactions and submitting suggestions.

## Main Functions

There are several main functions in this folder. Some of them are <SwmToken path="static/app/components/modals/sudoModal.tsx" pos="55:2:2" line-data="function SudoModal({">`SudoModal`</SwmToken>, <SwmToken path="static/app/components/modals/featureTourModal.tsx" pos="31:5:5" line-data="   * The FeatureTourModal will manage state on the active step.">`FeatureTourModal`</SwmToken>, HelpSearchModal, DiffModal, SuggestProjectModal, OverwriteWidgetModal, RecoveryOptionsModal, CreateNewIntegrationModal, DemoEndModal, and <SwmToken path="static/app/components/modals/createTeamModal.tsx" pos="15:2:2" line-data="function CreateTeamModal({Body, Header, ...props}: Props) {">`CreateTeamModal`</SwmToken>. We will dive a little into <SwmToken path="static/app/components/modals/sudoModal.tsx" pos="55:2:2" line-data="function SudoModal({">`SudoModal`</SwmToken> and <SwmToken path="static/app/components/modals/featureTourModal.tsx" pos="31:5:5" line-data="   * The FeatureTourModal will manage state on the active step.">`FeatureTourModal`</SwmToken>.

## <SwmToken path="static/app/components/modals/featureTourModal.tsx" pos="31:5:5" line-data="   * The FeatureTourModal will manage state on the active step.">`FeatureTourModal`</SwmToken>

The <SwmToken path="static/app/components/modals/featureTourModal.tsx" pos="31:5:5" line-data="   * The FeatureTourModal will manage state on the active step.">`FeatureTourModal`</SwmToken> function manages the state of a feature tour, including advancing through steps and handling user interactions. It uses a class component <SwmToken path="static/app/components/modals/featureTourModal.tsx" pos="136:2:2" line-data="class ModalContents extends Component&lt;ContentsProps, ContentsState&gt; {">`ModalContents`</SwmToken> to render the modal's content, including images, headers, and buttons for navigation. The modal also tracks the duration each step is open and triggers callbacks when the tour is advanced.

<SwmSnippet path="/static/app/components/modals/featureTourModal.tsx" line="136">

---

The <SwmToken path="static/app/components/modals/featureTourModal.tsx" pos="31:5:5" line-data="   * The FeatureTourModal will manage state on the active step.">`FeatureTourModal`</SwmToken> function manages the state of a feature tour, including advancing through steps and handling user interactions. It uses a class component <SwmToken path="static/app/components/modals/featureTourModal.tsx" pos="136:2:2" line-data="class ModalContents extends Component&lt;ContentsProps, ContentsState&gt; {">`ModalContents`</SwmToken> to render the modal's content, including images, headers, and buttons for navigation.

```tsx
class ModalContents extends Component<ContentsProps, ContentsState> {
  static defaultProps = defaultProps;

  state: ContentsState = {
    current: 0,
    openedAt: Date.now(),
  };

  handleAdvance = () => {
    const {onAdvance, openedAt} = this.props;
    this.setState(
      prevState => ({current: prevState.current + 1}),
      () => {
        const duration = Date.now() - openedAt;
        onAdvance?.(this.state.current, duration);
      }
    );
  };

  render() {
    const {Body, steps, doneText, doneUrl, closeModal} = this.props;
```

---

</SwmSnippet>

## Modal Endpoints

Endpoints of Modals

### <SwmToken path="static/app/components/modals/sentryAppDetailsModal.tsx" pos="70:1:1" line-data="  getEndpoints(): ReturnType&lt;DeprecatedAsyncComponent[&#39;getEndpoints&#39;]&gt; {">`getEndpoints`</SwmToken>

The <SwmToken path="static/app/components/modals/sentryAppDetailsModal.tsx" pos="70:1:1" line-data="  getEndpoints(): ReturnType&lt;DeprecatedAsyncComponent[&#39;getEndpoints&#39;]&gt; {">`getEndpoints`</SwmToken> function in the <SwmToken path="static/app/components/modals/sentryAppDetailsModal.tsx" pos="36:6:6" line-data="export default class SentryAppDetailsModal extends DeprecatedAsyncComponent&lt;">`SentryAppDetailsModal`</SwmToken> component defines the API endpoint to fetch the feature data for a specific Sentry app. This function returns an array with the endpoint URL, which is used to retrieve the features associated with the Sentry app.

<SwmSnippet path="/static/app/components/modals/sentryAppDetailsModal.tsx" line="70">

---

The <SwmToken path="static/app/components/modals/sentryAppDetailsModal.tsx" pos="70:1:1" line-data="  getEndpoints(): ReturnType&lt;DeprecatedAsyncComponent[&#39;getEndpoints&#39;]&gt; {">`getEndpoints`</SwmToken> function in the <SwmToken path="static/app/components/modals/sentryAppDetailsModal.tsx" pos="36:6:6" line-data="export default class SentryAppDetailsModal extends DeprecatedAsyncComponent&lt;">`SentryAppDetailsModal`</SwmToken> component defines the API endpoint to fetch the feature data for a specific Sentry app.

```tsx
  getEndpoints(): ReturnType<DeprecatedAsyncComponent['getEndpoints']> {
    const {sentryApp} = this.props;
    return [['featureData', `/sentry-apps/${sentryApp.slug}/features/`]];
  }
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBc2VudHJ5LWRlbW8tMSUzQSUzQVN3aW1tLURlbW8=" repo-name="sentry-demo-1" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
